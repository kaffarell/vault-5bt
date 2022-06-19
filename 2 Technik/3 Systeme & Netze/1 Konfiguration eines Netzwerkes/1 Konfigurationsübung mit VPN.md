![Aufbau](https://cdn.discordapp.com/attachments/613625981219110914/973506697987498004/unknown.png)

Wobei $R_4$ Router **7200** ist.
Die Toolbox agiert wie ein Webserver.
Ziel ist es, dass unser PC mittels eines VPNs den Webserver einer anderen Gruppe erreichen kann.

Zuerst muss $R_4$ auf $f2/0$ mit **DHCP** IP erhalten
```ad-info
ena
conf t
int f0/1
ip address dhcp
no sh
```

Danach muss $R_4$ auf $f0/0$ eine **statische** **IP** erhalten
```ad-info
ena
conf t
int f0/0
ip address 192.168.X.1 255.255.255.0
no sh
```
Das X ist die Nummer der Gruppe (in unserem Fall 1)

Anschließend wurde dem **PC** statisch die IP **192.168.X.2** und der **Toolbox** die IP **192.168.X.50** gegeben
```ad-info
Für PC muss folgender Befehl ausgeführt werden.
ip  <abbr title="IP Address">192.168.X.2</abbr> <abbr title="subnet mask">255.255.255.0</abbr> <abbr title="default gateway">192.168.X.1</abbr>

Bei der Toolbox muss man bei der Konfiguration auf "EDIT" klicken und den mittleren Block auskommentieren. Dort müssen dann IP und Gateway eingetragen werden.
```

Danach muss auf dem Router NAT/PAT eingerichtet werden
```ad-info
int $f0/0$
Ip nat inside
exit

int $f2/0$
ip nat outside
exit


access-list 1 permit <abbr title="Lokales Netzwerk">192.168.X.0</abbr> <abbr title="Wildcard">0.0.0.255</abbr>
ip nat inside source list 1 int <abbr title="Äußerer Port">f2/0</abbr> overload
```

Um den VPN einzurichten muss beim Router $R_4$ folgendes vorgenommen werden
```ad-info
crypto ipsec transform-set TRANS-ESP esp-3des esp-sha-hmac
crypto map CRYPTO_MAP 10 ipsec-isakmp
set peer <abbr title="Adresse des Netzwerkes eines Kollegen">10.10.30.100</abbr>
set transform-set TRANS-ESP
match address 100
int fa 2/0
crypto map CRYPTO_MAP
exit
access-list 100 permit ip <abbr title="Eigenes Netz">192.168.1.0</abbr> 0.0.0.255 <abbr title="INTERNES Netzwerk des Kollegen">192.168.4.0</abbr> 0.0.0.255
crypto isakmp key 0 teststring address 
```

### Webserver Konfigurieren
Es gilt einen Webserver aufzusetzen, welcher über ein statisches NAT im Netzwerk zugreifen kann. Ein statisches NAT wird benötigt, damit der Webserver immer mit der gleichen IP erreicht werden kann.

Bild

Mit dem Webterminal wurde getestet ober der Webserver (Toolbox) im lokalen Netz zugänglich ist. Als dies bestätigt wurde, wurde ein statisches NAT für den Webserver eingerichtet.

```ad-info
ip nat inside source static <abbr title="Eigene Lokale IP des Webservers">192.168.1.50</abbr> <abbr title="IP im öffentlichen Netz zu der es werden soll">10.10.30.200</abbr>
```
Wir haben mittels ping sicher gestellt, dass 10.10.30.200 noch nicht vergeben war.
```ad-info
ip name-server 10.10.30.1
ip domain-lookup
```
Anschließend wurde bei der Toolbox unter /var/www/html die index.html bearbeitet um die Website zu personalisieren.




Es wurde ein UbuntuDocker ([[1 Docker|Docker]]) als Gerät bei GNS3 installiert.
Der zweck dessen war, um dieses als ssh-Verbindung zu nutzen, jedoch musste dadurch erst eine Verbindung ins Internet hergestellt werden um um das ssh package zu installieren.



# Zusammen erarbeitetes
Gruppe 0 (= X)
Router 7200 mit PC und Cloud verbinden
Ziel: PC1 ins SN-Lab Netzwerk kommen

Anfangs Ports zu Router hinzufügen
Danach DHCP Server bei Router für privates Netzwerk konfigurieren
```ad-info
ip dhcp excluded-address 192.168.X.1 192.168.X.100
ip dhcp pool snlabX
Network 192.168.X.0 255.255.255.0
default-router 192.168.X.1
dns-server 8.8.8.8

int fa0/0
ip address 192.168.X.1 255.255.255.0
no sh
```

Adressen von 0.1 bis 0.100 sind ausgeschlossen weil diese sonst verwendet werden

DHCP pool definiert das Netzwerk, für welches IPs vergeben werden sollen.

Bei PC1
```ad-info
ip dhcp
```

Bei Router:
Bei int f1/0 mit dhcp eine Adresse zugewiesen bekommen
```ad-info
int f1/0
ip address dhcp
no sh
```

Erhaltene IP 10.10.30.78
PAT konfigurieren, damit der PC ins SN-Lab kommt
```ad-info
ip nat inside source list 5 interface f1/0 overload
access list 5 permit 192.168.X.0 0.0.0.255
```
Jeder PC im Netzwerk 192.168.X.0 wird für PAT allowed
```ad-info
int f0/0
ip nat inside
int f1/0
in nat outside
```
Nun kann PC1 ins SN-Netzwerk

Webserver von außen sichtbar machen
Toolbox konfigurieren:

Mit rechtsklick auf configure --> edit --> IP, etc. angeben
up echo nameserver 8.8.8.8 (um ins internet zu kommen)
Ip auf X.50
Statisches PAT für den Webserver einrichten
```ad-info
ip nat inside source static tcp 192.168.X.50 80 10.10.30.78 80
ip nat inside source static tcp 192.168.X.50 443 10.10.30.78 443

```
Port 80 und 443 von X.50 wird auf Port 80 und 443 von 30.78 weitergeleitet

Bei Toolbox muss mit OpenSSL ein Zertifikat für HTTPS erstellt werden
```ad-info
apt install openssl
mkdir /etc/nginx/certificate
cd /etc/nginx/certificate
openssl req -new -newkey rsa:4096 -x509 -sha256 -days 365 -nodes -out -nginx-certificate.crt -keyout nginx.key
```
Mit diesem Befehl wird ein Public key (Zertifikat) und und ein Private key erstellt

NGINX konfigurieren um SSL zu verwenden
```ad-info
sudo nano /etc/nginx/snippets/self-signed.conf
```
In der Datei müssen folgende  Zeilen hinzugefügt werden
```ad-info
listen 80 ssl default_server; --> listen 443 ssl default_server;
ssl_certificate /etc/nginx/certificate/certificate.crt
ssl_certificate_key /etc/nginx/certificate/nginx.key
```

IP-Sec ist eine Verbindung zwischen 2 Privaten Netzwerken über ein Öffentliches Netzwerk
IP-Sec für VPN einrichten:
Als erstes muss Crypto erstellt werden
Welcher Hash algorithmus & Gruppe verwendet wird muss bei beiden gleich sein.
Erster Kanal um Infos über Tunnelaufbau auszutauschen (unverschlüsselt) (isakmp)
Zweiter Kanal um wirklich Daten auszutuaschen, wenn Tunnel aufgeabut ist (verschlüsselt) (3des/sha)
Erster Kanal wird nicht abgebaut, es werden periodisch neue Schlüssel ausgetauscht welche automatisch generiert werden. Teststring wird nur verwendet um den Tunell zum ersten mal aufzubauen.

```ad-info
title: Erster Kanal
crypto isakmp policy 10
hash md5
authentication pre-share
group 2
encryption 3des
crypto isakmp (key 0) teststring address 10.10.30.Y
```
Y stellt hier die Adresse der anderen Person dar.
key 0 wird nicht bei allen routern benötigt

```ad-info
title: Zweiter Kanal
crypto ipsec transform-set TRANS-ESP esp-3des esp-sha-hmac
```
TRANS-ESP ist eine liste mit Parametern für den zweiten Kanal
3des ist zur verschlüsselung und sha zum hashen

Policy, group und transform-set werden nun in eine crypto-map gebündelt.
10 ist hier die policy von vorher.
```ad-info
crypto map CRYPTO_MAP 10 ipsec-isakmp
```
Angeben zu wem man IP-Sec aufbauen möchte

Y ist das Netzwerk des Kollegen
X und Y müssen dabei anders sein, weil es sonst zu konflikten kommt.
Das erste ist source und das zweite destination.
```ad-info
access-list 100 permit ip 192.168.X.0 0.0.0.255 192.168.Y.0 0.0.0.255
set transform-set TRANS-ESP
match address 100
```
Diese Crypto-Map muss nun an ein interface gebunden werden
```ad-info
int f1/0
crypto map CRYPTO_MAP
```

Mit folgendem Befehlt kann überprüft werden ob der erste Kanal aufgebaut wurde.
```ad-info
do show crypto isakmp sa
```
Bis kein Ping geschickt wurde, wird keine Verbindung aufgebaut.
Es muss jedoch vom PC aus gepingt werden, da der Router im 10.10.30.0 Netzwerk ist.

Mit dem debug Befehl können evtl. Fehler ausfindig gemacht werden.
