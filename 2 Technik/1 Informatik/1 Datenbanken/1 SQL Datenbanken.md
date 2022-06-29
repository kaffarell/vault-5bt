# SQL Datenbanken

* Arbeiten mit Transaktionen
* ACID Prinzip ->
	* Atomar
	* Consistent
	* Isolation
	* Durability
	
	auch [[5 Theorie|hier]]
	**Atomar**: Die Transaktion wird immer ganz oder gar nicht ausgeführt. Das bedeutet keine Transaktion kann teilweise ausgeführt werden.
	**Consistent**: Vor und nach der Transaktion ist die Datenbank konsistent (dh: Die Datenbank muss funktionsfähig sein und die Daten müssen integer sein).
	**Isolation**: Mehrere Transaktionen können gleichzeitig ausgeführt werden ohne dass eine die andere Beeinflusst.
	**Durability**: Wenn die Transaktion successful ist dann werden die Änderungen immer zur Datenbank geschrieben
	