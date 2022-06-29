Zwei Arten von Verschlüsselungen:
- **Symmetrische Verfahren**
	- Zum verschlüsseln und entschlüsseln verwendet man den gleichen Schlüssel
	- Beispiel: DES, 3DES, AES
- **Asymmetrische Verfahren**
	- Zwei verschiedene Schlüssel (public key, private key)
	- Zum verschlüsseln benützt man den public key (der ist für alle verfügbar)
	- Zum entschlüsseln benützt man den private key (darf nicht veröffentlicht werden)
	- Beispiel: RSA

## Kerckhoffs' Maxim
"Die Sicherheit eines Kryptosystems darf nicht von der Geheimhaltung des Algorithmus abhängen. Die Sicherheit gründet sich nur auf die Geheimhaltung des Schlüssels."

## Symmetrische Verschlüsselung
- Einen schlüssel zum entschlüsseln und verschlüsseln
- Vorteil: ist schnell
- Nachteil: der schlüssel muss sicher vom sender zum empfänger gelangen

### Schlüsselaustausch
- Diffie Hellmann
- Auf einen gemeinsamen Schlüssel kommen ohne ihn nie ausgetauscht haben
![[diffie-hellmann.png]]
- Beide kommen auf der Geheimzahl 10 ohne sie nie übertragen zu haben

## Asymmetrische Verschlüsselung
- public key und private key werden zufällig generiert
- Vorteil: beide haben nicht den gleichen Schlüssel
- Nachteil: sind langsam (1000 mal langsamer als symmetrisch)

- Öffentlicher Schlüssel
	- Für jeden zugänglich
	- Kann Daten nur verschlüsseln
	- Kann digitale Signature prüfen
	- Kann jemanden authentifizieren

- Private Schlüssel
	- Sollte nur eine Person besitzen
	- Kann Daten entschlüsseln
	- Kann eine digitale Signatur erstellen
	- Man kann sich dadurch authentifizieren
	
	
	
## Beispiel: TLS
- HTTPS verschlüsselt alle verbindungen
- Benützt dazu TLS (wurde früher SSL genannt) (Transport Layer Security)
- TLS nutzt asymmetrische und symmetrische Verschlüsselung um das beste von beiden zu bekommen: Geschwindigkeit und Sicherheit.
- TLS 1.3 benützt  normalwerweise RSA(asymmetrisch) und AES(symmetrisch)

### TLS Handshake
- Server generiert pub und priv key
- Server schickt unverschlüsselt zufällig generierte Zahl dem Client (server secret)
- Client schickt unverschlüsselt zufällig generierte Zahl dem Server (client secret)
- Client generiert zufällige zahl (premaster secret), verschlüsselt es mit pub key vom Server und schickt es dem Server.
- Aus dem server secret, client secret und premaster secret wird eine session key generiert (Beide server und client sollte auf der selben session key kommen)
- Dann wird immer mit AES(symmetrisch) und der session key verschlüsselt kommuniziert. (Jetzt kann auch pub und priv key gelöscht werden, weil es sie nicht mehr braucht, jetzt wird nur noch symmetrisch kommuniziert)


## RSA
siehe: [[3 RSA|RSA bei TP]]

## AES
- nachfolger von DES
- verschiedene Schlüssellängen: 128 bit, 192 bit, 256 bit (desto länger desto sicherer)