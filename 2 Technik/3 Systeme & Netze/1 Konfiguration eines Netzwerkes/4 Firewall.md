* Viele Router und Betriebssysteme haben eine Firewall-Funktion integriert
	* z.B. cisco firewall oder Windows Firewall
* Es gibt auch Open Source Firewalls
	* pfSense
	* IpFire


### Wir haben mit pfSense übungen gemacht
* Mit pfSense kann man bestimmte Regeln definieren
	* z.B.:
		* Blockiere alle pinsg vom PC1 zum Webserver.
		* Blockiere alle pings vom PC1 ins Internet.
		* Blockiere alle http Anfragen vom Webserver zur www.fallmerayer.it Seite.
		* Blockiere für den Webserver die https://www.google.de Seite.

## Arten von Firewalls
* STATEFUL FIREWALL 
	* Das ganze paket mit inhalt wird angeschaut
	* Speicher gute und schlechte verbindungen (damit in der zukunft zurückgeschaut werden kann)
* STATELESS FIREWALL:
	* Nur statische informationen wie source und destination werden angeschaut
	* Speichert keine connections und informationen
	
Normalerweise sind alle firewalls Stateful