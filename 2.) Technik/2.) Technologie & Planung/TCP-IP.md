# TCP/UDP



## TCP
- min 536 Bytes
- max 1452 Bytes

### Ports
- well known ports
		- 80: http
		- 20 und 21: ftp
		- 22: ssh
		- 443: https
## Verbindungsablauf
- Verbindungsaufbau
- Datentransfer
- Verbindungsabbruch

### Three Way Handshake
![3way_handshake](https://cdn.discordapp.com/attachments/818403821599457280/974265488299417620/unknown.png)
- Sendet Syn Flag + Zufallsnummer (Sequence Number)
- Empfängt Syn Ack + Acknumber (seq number + 1)

### Stop and Wait
- jedes Paket wird bestätigt
![Stop and Wait](https://cdn.discordapp.com/attachments/818403821599457280/974265472088432690/unknown.png)

### Sliding Windows

### TCP Flusskontrolle