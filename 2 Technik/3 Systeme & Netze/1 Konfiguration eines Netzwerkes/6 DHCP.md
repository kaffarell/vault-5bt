* Manuell 
	* Statisches DHCP 
	* MAC bekommt bestimmte IP 
	* IPs gelten auf unbestimmte Zeit 
	* Nachteil: Keine neuen Clients 
	* Vorteil: Wenn sich Netzwerk nicht ändert 
* Automatisch 
	* Server weißt ein Mal IPs zu --> Sie ändern sich nicht 
	* Am DHCP-Server wird Bereich von IPs definiert 
	* Neue Clients bekommen neue IP 
	* Zuordnung wird nicht verändert 
	* Unwichtiger als Manuell & Dynamisch 
	* Begrenzte Anzahl von Clients 
* Dynamisch 
	* Gleich wie Automatisch nur mit Leihdauer 
	* Meldet sich Client nicht, wird IP freigegeben 


* DORA: 
	* Discover:
		* Von Client an Server 
		* Dest Mac = Broadcast (FF:FF) 
	* Offer:
		* Server schickt Anfrage an Client 
		* Dest Mac = Client 
	* Request:
		* Client requestet IP 
		* Dest Mac = Server Mac 
	* Acknowledge:
		* Server erteilt Erlaubnis 
		* Dest Mac = Client 
		
	* Config:
		* Router:
```cmd
ip dhcp excluded-address UntereIP ObereIP 
ip dhcp pool name 

--> Im pool: 
network 129.168.10.254 255.255.255.0 
default-router 192.168.10.1 
(optional) dns-server 8.8.8.8
```
DHCP Probleme: Konfiguration funktioniert nicht wenn in anderem Subnetz 2 Lösungen: Jedes Subnetz hat DHCP-Server Man definiert Helper-Adressen Gegebene Adresse gibt DHCP weiter