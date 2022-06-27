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
Docker benützt ein feature des Linux Kernels um container zu erstellen: namespaces.
Mit namespaces kann man isolierte Ressourcen erstellen, die andere Ressourcen nicht sehen können.
Zum Beispiel kann ein neuer Prozess in einem namespace gestartet werden -> Der Prozess sieht so keien anderen Prozess auserhalb des namespaces und ist innerhalb isoliert. Wenn dieser Prozess neue Prozesse startet landen diese auch im gleichen namespace. Mit namespaces erstellt man praktisch eine art sandbox, wo der beinhaltete prozess dem Host OS nichts anhaben kann und nichs verändern kann.

Wenn ein docker container gestartet wird, wird die darin enthaltene Applikation also in einem neuen namespace gestartet.

Container „fühlen sich an“ wie VMs sind aber Prozesse bzw. Prozessgruppen

Als Beispiel habe ich hier nur den pid(Prozess)-Namespace benützt, aber es gibt auch namespaces für user, files und ordner (mnt), network (net) etc..


## cgroups
cgroups ist auch ein feature des Linux Kernels.
Mit cgroups kann man bestimmten Prozessen CPUs,etc.. zuweisen.
Zum Beispiel kann ich einstellen, dass der Prozess mit der pid 5 maximal 5 GB speicher bekommt und 20% CPU nutzen kann.

## docker swarm
Mit docker swarm kann man mehrere PCs zusammenhängen und auf allen PCs docker container ausführen.
Wenn dann zum Beispiel 2 container auf einen PC gestartet werden, verschiebt sich ein container automatisch auf den anderen PC. (Die container werden auf den PCs aufgeteilt).

Wenn ein container abstürzt wird er außerdem automatisch neu gestartet.

docker swarm ist ein sogenannter "Orchestrator". -> "Dirigiert" mehrere container über mehreren PCs

# Hypervisor (VMWare)