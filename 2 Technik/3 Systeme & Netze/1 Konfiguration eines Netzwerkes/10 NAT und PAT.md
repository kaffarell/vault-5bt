# NAT & PAT
## NAT
NAT = Network Address Translation

- Wandelt eine private IP-Adresse in einer öffentlichen um
- Dazu braucht es einen NAT-Router

- Man kann nicht einfach jeden PC auf der Erde eine öffentlich IP geben (weil es zu wenige gibt)
- Wenn ich deswegen einen öffentlichen Dienst in einem anderen Netz benützen will, wird meine private IP-Adresse in einer öffentlichen umgewandelt
- Der NAT-Router wandelt also viele private IP-Adressen in einer öffentlichen um
- Dabei verändert er nur das Feld der destionation und source IP


![[nat.png]]

Die öffentliche IP des Routers ist hier 82.6.4.2

- NAT verbessert auch die Sicherheit, denn so kann der externe Server nicht auf dem lokalen PC zugreifen (kennt die private IP nicht, und kann auch mit der privaten IP nicht darauf zugreifen)


## PAT
- Das Problem bei NAT ist, dass wenn mehrere PCs in einem private Netz sind, finden die pakete nicht den richtigen PC auf dem Weg zurück
- Deswegen wird auch die Port-Nummer verändert und jeder PC bekommt eine eigene port nummer
- Der router hat dann eine tabelle und speichert alle port-nummern und den dazugehörigen PC ab -> so kann er von der Port nummer auf der private adresse des PCs schließen