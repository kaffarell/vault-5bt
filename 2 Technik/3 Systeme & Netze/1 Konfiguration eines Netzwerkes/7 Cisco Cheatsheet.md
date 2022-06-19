**Set password for router serial port:

-   ena
    
-   config
    
-   line config 0
    
-   password cisco
    
-   login
    

-   exit
    
-   exit
    
-   exit
    

Dann muss man login machen

Password für ena mode (enable) setzen:

-   ena
    
-   config
    
-   enable password cisco
    

Password set!

In config datei (do sh running-config) sieht man passwörter im klartext,

Deswegen sollten sie verschlüsselt werden.

-   ena
    
-   config
    
-   service password-encryption
    

Dann sind die Passwörter in der Config-Datei verschlüsselt (sh running-config)

### Config Router Port

-   ena
    
-   config
    
-   interface
    
-   interface Fa0/0
    
-   ip address 10.10.10.1 255.255.255.0
    
-   no shutdown
    

### Setup Router for Telnet Access

-   ena
    
-   config
    
-   line vty 0
    
-   password cisco
    
-   login
    

On PC:

-   telnet 10.10.10.1
    

Save Config for Router

-   write
    

### Switch IP Adresse

Normalerweise leitet ein switch nur daten weiter. Man kann ihm aber auch eine ip adresse  geben.

-   conf t
    
-   int vlan 1
    
-   ip address 1.1.1.100 255.255.255.0
    
-   no sh
    

(in ena mode)

-   show mac-address-table
    

Zeigt die arp tabelle

### Static IP Routing

target-ip  mask  next-hop

-   ip route 10.0.0.0 255.255.255.0 192.168.0.253
    

  

Show routes

-   show ip static-route
    

  
  
  

### SSH Server

SSH Server auf router installieren

-   ena
    
-   conf
    

Hier eine domain name auswählen

-   ip domain-name snlab.local
    

Hostname ändern (name ist beliebig)

-   hostname router1
    

Jetzt müssen die Schlüssel generiert werden:

  

-   crypto key generate rsa
    

Dann muss die länge eingegeben werden (sicher ist 2048)

Key anzeigen:

(in ena mode)

-   sh crypto key mypubkey rsa
    

  

(optional muss man auch password enablen: enable password admin)

  

Neuen User erstellen:

-   username admin password admin
    

Um mit telnet oder ssh zu verbinden brauche ich eine virtuelle vty line.

Vty Line auswählen:

-    line vty 0 15
    

Konfiguriert alle lines von 0 bis 15

  

(optional ssh version 2 verwenden: ip ssh version 2)

Verbindungsmethode feststellen (erlauben):

-   transport input ssh
    

User für ssh verbindung auswählen. Nimmt in diesem Fall einen lokalen Benutzer und ein lokales Passwort

-   login local
    

Zeigt konfiguration an:

-   do show running-config
    

SSH status anzeigen mit: (ena mode)

-   sh ssh
    

  
  

### Vlan setzen

-   ena
    
-   conf t
    

Neuen vlan erstellen

-   vlan 10
    

name des vlans ändern

-   name snlab
    

Vlan löschen:

-   no vlan 20
    

Dann mit

-   int FastEthernet 0/2
    

Zum port wechseln

Angeben dass an diesem port ein pc hängt

-   switchport mode access
    

PC wird zum vlan hinzugefügt

-   switchport access vlan 10
    

Alle vlans mit PCs anzeigen

-   do sh vlan brief
    

Switchport mode wird auf trunk gyesetzt wenn ein switch daran hängt

-   switchport mode trunk
    

Lässt den vlan 10 durch den trunk durch

-   switchport trunk allowed vlan 10
    

Wenn man neue einträge hinzufügt muss man

-   switchport trunk allowed vlan add 30
    

Ausführen

  
  
  

### DTP

  

Dynamic Trunking Protocol

Erstellt automatisch trunks zu anderen Switches. (ist ein Sicherheitsproblem, denn ein Hacker kann sich selber zum Trunk wählen und alle Frames abfangen)

### Router on a stick

Auf dem Router:

Interface einschalten

Conf t

Int fa0/0

No sh

Subinterfaces für beide VLANs machen (10, 20)

Int fa0/0.10

Encapsulation dot1q 10

Ip address 10.1.10.1 255.255.255.0

Int fa0/0.20

Encapsulation dot1q 20

ip address 10.1.20.1 255.255.255.0

Beim Haupt switch:

Conf t

Int fa0/1

Switchport mode trunk

  
  

### OSPF konfigurieren

Auf allen routern muss ausgeführt werden:

-   ena
    
-   conf t
    
-   router ospf 1
    

1 ist die process-id, muss bei jedem router eine andere zahl sein

dann die netzwerke die direkt angehängt sind

-   network 3.3.3.0 255.255.255.0 area 0
    

Wenn alle Netzwerke in diesem Netz zusammenhängen sollen, dann sollen alle die gleiche Area haben

Bei besonders großen netzen werden unterschiedliche Areas verwendet, damit alle Router nicht so viel Leistung brauchen (Dijkstra Algorithmus).

OSPF Konfiguration anzeigen mit

-   sh ip ospf
    

Alle erkannten Netzwerke anzeigen mit:

-   sh ip ospf neighbor
    

Die OSPF Nachbarn werden in einer Datenbank gespeichert. Die Datenbank kann so ausgegeben werden:

-   sh ip ospf data
    

  
  
  

### Konfiguration RIP Routing

  

Bei allen Routern das Protokoll aktivieren:

-   router rip
    

  

Dann bei allen Routern die benachbarten Netzwerke angeben:

-   network <neighbor network dass man freigeben will>
    

zB.:

-   network 192.168.1.0
    

  

Optional, falls ein switch an einem Port angehängt ist, diesen Befehl ausführen:

-   passive-interface fastEthernet 0/0
    

Somit werden keine rip-pakete an den switch geschickt

  
  

DHCP Server aufsetzen

  

ena

conf t

  

Zum Ausschließen von bestimmten Adressen, eignet sich wenn bestimmte Adressen für Server oder NAS reserviert sein müssen.

-   ip dhcp excluded-address <low-ip> <high-ip>
    

oder

-   ip dhcp excluded-address <ip>
    

  

DHCP aufsetzen

-   ip dhcp pool <name>
    
-   network <ip-netzwerk> <maske-netzwerk>
    
-   default-router <gateway-addresse>
    
-   dns-server 8.8.8.8
    

  

Show dhcp statistics

-   show ip dhcp server statistics
    

  
  

(Lösungen Arbeitsblatt: [https://www.pressexam.com/8-1-3-3-packet-tracer-configuring-dhcpv4-using-cisco-ios/](https://www.pressexam.com/8-1-3-3-packet-tracer-configuring-dhcpv4-using-cisco-ios/))

  

### NAT / PAT 

-   access-list 1 permit 10.10.10.0 0.0.0.255
    
-   ip nat inside source list 1 interface Serial 2/0 overload
    

Mit diesem befehl werden alle ip adressen umgewandelt und alle bekommen die gleiche öffentlich ip, mit overload werden ports zugewiesen zu den IP adressen um sie danach zu einem PC zuzuordnen

  

-   int fastEthernet 0/0
    
-   ip nat inside
    

  
  

### Link Aggregation

![](https://lh3.googleusercontent.com/fohurTVdXy6jBgvkrsc_M8TjoWEqpjx7nIhZkCW_Prlgwy_oaNTD2ZTCcWIOjWPDD0jbuQ8iPpXpGoF_DTFzIjsBgiGsl4oUJ7Zyoin7DYpwKQ70QIgTswup0iU2SBKIsv8ndND81myc2yHorA)

EtherChannel LAPD configuration:

  

-   interface range FastEthernet0/1 - 2
    
-   channel-group 1 mode active
    
-   interface port-channel 1
    

  

-   switchport mode trunk
    
-   switchport trunk allowed vlan 1
    

  

Andere wichtige EtherChannel befehle:

-   show etherchannel summary
    

![](https://lh4.googleusercontent.com/7m5Fcuc4JPllT-aSL8Nvppf5RJp1YW9ui0eKtw4KSPnpFpn6Sjk6SQXOAej507VJY-0xJUYNBYIgyT1w3tBvDJSTyybG4A1kxdCfW8sXmd8jKH0SyVJRXv5BLKzxTcoJ70sKOE_9056ovAicjA)**