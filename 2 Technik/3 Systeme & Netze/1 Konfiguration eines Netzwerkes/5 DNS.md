1) Ein DNS-Dienst wandelt Domain-Namen (z.B. google.com) in einer IP-Adresse um.  

2) Ein Domain-Name besteht aus einer subdomain (z.B www), aus einem domain-name oder hostname (zB.: google) und eine TLD (Top-Level-Domain) (z.B. .com).  

3) Eine Top-Level-Domain ist die Endung eines domain-names also zB.: com, org, it. Sie werden genutzt um dns-einträge besser aufzuteilen.  

4) Das DNS-System das wir im Moment haben, sieht aus wie eine Baumstruktur und jeder Server definiert eine DNS-Zone welche der Server definiert. zB gibt es Server die die .com zone definieren und welche die die .org zone definieren.  

![[dns.png]]

5) DNS-Server haben ihre Einträge in sogenannte Records abgespeichert. Es gibt dabei verschiedene Record-types: 

	* A  
		* Ein A Record zeigt direkt auf einer IPv4 Adresse zB.: www.google.com -> 182.46.3.7  
	* NS  
		*	Ein NS Record zeigt auf einem anderen Nameserver, der diesen Namen definiert z.B:  
			www.google.com -> .com tld server (Es verweist auf einen anderen Server, der alle  
			Einträge mit der .com Endung hat)  
6)  Es gibt insgesamt 13 Root-server, die viele NS-Einträge haben. Sie haben eine Liste mit alle top level domain namen die es gibt. (z.B.: com, it, de...). Ein Authorative DNS-Server speichert Records, die permanent abrufbar sind, ein non-authorative server speichert keine Records, er cached nur dns-abfragen oder leitet sie im Fall weiter zu einem anderen Server.  

Really cool video: https://youtu.be/vrxwXXytEuI  
Facebook DNS outage explained (also explaines dns really well):  
https://youtu.be/-wMU8vmfaYo  

### Lookup  
```bash
nslookup wikipedia.org a.root-servers.net  
```
Lookup for wikipedia.org on a root-server. As we see we can only find a redirect to the org gtld-servers (global top level domain servers). If we query that  
```bash
nslookup wikipedia.org a.gtld-servers.net  
```
we can find another redirect to a wikipedia dns server named ns01.wikipedia.org.  

### Another Lookup
List of root-servers: https://www.iana.org/domains/root/servers  
With the dig command we can execute (in linux we don't need the quotation marks):  
```bash
dig "@a.root-servers.net" google.com  
dig "@216.239.34.10" google.com  
```
Before the record we can find a type of record:  
* A (AAAA)
* NS
* CNAME

(There are many more, but these are the most important)  
A (when using ipv6 also AAAA) resolves directly to a ip address (f.e: google.com → 192.51.2.5)  
NS resolves to another nameserver (f.e: google.com → a.gtld-servers.net (a .com top level dns  
server))  
CNAME records hold an alias for another nameserver.  
(Difference between CNAME and NS is explained here:  
( https://webmasters.stackexchange.com/questions/78181/understanding-cname-and-ns-in-dns))  
There are also a few types of DNS-Servers:  
* Authorative DNS Server  
	An Authorative Server holds actual records and stores them (forever)  
* Non-Authorative DNS-Server  
	A Non-Authorative Server does not serve or hold any records. It can lookup in other dns-  servers automatically for records and relay them or it can cache specific dns-queries. (Most ISP have a default non-authorative dns server which caches all requests)  
	* Recursive DNS-Server
	* Cacher
	* Forwarder