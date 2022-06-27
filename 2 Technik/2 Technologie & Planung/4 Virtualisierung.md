Praxis zu Docker ist hier: [[1 Docker|Docker (SN)]]

# Docker
Mit Docker kann man Programme in kleine Virtuelle Maschinen packen, und diese auf allen PCs ausführen.

**Achtung, ist *ähnlich* aber nicht dasselbe wie Virtuelle Maschienen.**

Wenn ein Programm mit Docker ausgeführt wird, nennt man es einen **container**. Ein **image** beschreibt hingegen wie ein container erstellt wird.

Unterschied zwischen VMs und Docker:
![[container_vms.png]]
Wie man hier sieht, sind bei einer Applikation, die mit Docker ausgeführt wird, viel weniger schichten zur physischen Hardware. Das bedeutet Docker container sind viel schneller und einfacher aufzusetzen als eine VM.

Vorallem weil bei Docker das Betriebssystem fehlt. Es gibt nur ein Betriebssystem(Host OS). Bei einer VM gibt es hingegen das Host OS und das Guest OS.

Wichtig ist, dass bei beiden Modellen, bei der VM und bei Docker alle Apps isoliert sind. Das bedeutet App A kann nicht auf App B zugreifen. App A kann auch nicht auf das Host OS zugreifen (Ist für security wichtig -> docker container sind sehr sicher).

## namespaces


## cgroups
## docker swarm

# Hypervisor (VMWare)