![DMZ](https://cdn.discordapp.com/attachments/852214113949450270/978565569899036712/2022_05_24_09_49_Office_Lens.jpg)

Ziel ist es in der [[3 DMZ|DMZ]] einen Webserver zu haben, welcher von Außen zugänglich ist aber die [[3 DMZ|DMZ]] soll nicht ins LAN kommen.

Zuerst wurde Bei Router außen mit [[6 DHCP|DHCP]] eine IP vergeben
```ad-success
title: 
ip address dhcp
```

Danach wurde gePATtet und ein statisches PAT für den Webserver eingerichtet
```ad-success
title: 
ip nat inside source list 5 interface f1/0 overload access list 5 permit 192.168.X.0 0.0.0.255
```
```ad-success
title: 
int f0/0 ip nat inside int f1/0 in nat outside
```
```ad-success
title: 
ip nat inside source static tcp 192.168.X.50 80 10.10.30.78 80 ip nat inside source static tcp 192.168.X.50 443 10.10.30.78 443
```

Nun wurde die [[4 Firewall|Firewall]] mit PFSense eingerichtet
Der erste Port und IP muss mittels der Konsole konfiguriert werden. Alle folgenden können mittels des WebInterfaces konfiguriert werden
- User: Admin
- Password: pfsense

### MATURAFRAGE:
VERSCHIEDENE ARTEN VON [[4 Firewall|FIREWALLS]] : [[4 Firewall#Arten von Firewalls]]
