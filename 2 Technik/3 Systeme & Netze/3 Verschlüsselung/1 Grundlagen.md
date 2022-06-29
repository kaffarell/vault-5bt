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