e# NoSQL
* BASE Prinzip (BASE ist das gegenprinzip zu ACID ([[1 SQL Datenbanken|SQL Datenbanken]]))
	* **Basically Available** Immer Erreichbar
	* **Soft State** 
		State/Daten können sich ohne User Input ändern. [[1 SQL Datenbanken|SQL Datenbanken]] haben ein Hard State -> Daten ändern sich nicht ohne Input.
	* **Eventually Consistent** 
		Sind vielleicht nicht immer gleich konsistent sondern erst später.
		Beispiel -> Wenn ich etwas in der Datenbank eintrage und gleich später alles ausgebe, kann es sein dass die eingetragenen Daten noch nicht ausgegeben werden -> später schon
		NoSQL Datenbanken werden mit der Zeit konsistent -> [[1 SQL Datenbanken|SQL Datenbanken]] sind immer konsistent


## Beispiele:
* [[3 MongoDB|MongoDB]]
* Couchbase
* Redis
