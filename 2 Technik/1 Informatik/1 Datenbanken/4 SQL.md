```toc
```

## Tabellen erzeugen
Tabelle erzeugen wenn keine andere mit den gleichen Namen existiert.

Wenn eine andere Tabelle existiert wird ein Warning returned. (Ohne IF NOT EXISTS wird ein Error returned)

```sql
CREATE TABLE IF NOT EXISTS Personal  
(  
PersID int,  
    Vorname varchar(45),  
    Nachname varchar(45),  
    Gehalt double  
);
```

  
## Daten einfügen
Mit dem INSERT INTO Befehl können Daten in Tabellen hinzugefügt werden.

```sql
INSERT INTO Personal (PersID, Vorname, Nachname, Gehalt) VALUES (0, "Alex", "Unterleitner", 200.00);
 ``` 

Mit dem SELECT Befehl kann geschaut werden, ob das INSERT funktioniert hat. (Unten kommt mehr zu den Abfragen und zu SELECT)

```sql
SELECT * FROM Personal;
```


## Tabellen/Daten ändern
Spalten löschen:

```sql
DELETE FROM Personal WHERE (Nachname="Mueller" AND PersId=5)
```

  

Spalte updaten:

(Achtung, das würde alle Namen ändern!)

```sql
UPDATE Personal SET Name="Joggl"
```

Um spezifische spalten zu ändern:

```sql
UPDATE Personal SET Name="Joggl" WHERE PersId=6
```
  

Spalte (Attribut) zu Tabelle hinzufügen

```sql
ALTER TABLE `table_name` ADD COLUMN `column_name` `data_type`;
```
  
## Constraints
Constraints (Beschränkungen für attribute):

```sql
CREATE TABLE table_name (  
    column1 datatype constraint,  
    column2 datatype constraint,  
    column3 datatype constraint,  
    ....  
);  
```
  

Alle constraints:

* `PRIMARY KEY`
* `NOT NULL`  
* `FOREIGN KEY`
* `UNIQUE`
* `CHECK`
* `DEFAULT`
* `AUTO_INCREMENT`

Man kann einem Constraint auch einen Namen geben:
```sql
CREATE TABLE Persons (  
    ID int NOT NULL,  
    LastName varchar(255) NOT NULL,  
    FirstName varchar(255),  
    Age int CHECK (Age>18),  
    CONSTRAINT UC_Person UNIQUE (ID,LastName)  
);
```
  

### Foreign keys
Tabelle mit zwei fremdschlüsseln zu einer anderen Tabelle erzeugen:
```sql
CREATE TABLE Internships (  
    PersId INT PRIMARY KEY,  
    duration INT,  
    tutorId INT,  
    FOREIGN KEY(PersId) REFERENCES People(id),  
    FOREIGN KEY(tutorId) REFERENCES People(id)  
);
```
  

Will man zu den Foreign keys noch mehr Regeln hinzufügen, muss man einen Constraint erzeugen:
```sql
CONSTRAINT PersId_Constraint  
    FOREIGN KEY (PersId)  
    REFERENCES People(id)  
    ON DELETE CASCADE  
);
```
  

Andere mögliche zusätzliche Regeln:
```sql
[ ON UPDATE { NO ACTION | CASCADE | SET NULL | SET DEFAULT } ]
```
  

Wenn man ON DELETE CASCADE dazugibt dann wird der Eintrag in Internships gelöscht, wenn die Person mit der PersId in dem Parent-table people gelöscht wird.

CASCADE bedeutet dass die Kinder geupdated wer

Wenn man ein den. Anstatt CASCADE kann man auch SET NULL benützen, dann werden die Kinder auf NULL gesetzt oder SET DEFAULT, dann werden die Kinder auf default gesetzt.

  
  

#### ON DELETE

Wenn der parent gelöscht wird, wird das child mit gelöscht. Gibt an was mit dem Child passieren soll, wenn der Parent gelöscht wird. Es gibt NO ACTION, CASCADE, SET NULL und SET DEFAULT als Optionen. 

  
#### ON UPDATE

Optional. Gibt an was mit dem Child passieren soll, wenn der Parent geupdatet wird. Es gibt NO ACTION, CASCADE, SET NULL und SET DEFAULT als Optionen. 

  

#### NO ACTION 
(Ist die default Einstellung, also auch wenn man es nicht schreibt)

Wir zusammen mit ON DELETE oder ON UPDATE benutzt. Wenn versucht wird den Parent zu updaten oder zu löschen, dann funktioniert es nicht und es kommt ein Fehler. Parent und Child bleiben gleich. Ist nützlich als Sicherheit bei sehr wichtigen Datenbanken z.B. Bank und Bankkontos.

Auch wenn die Bank gelöscht wird, muss erster geschaut werden, was mit den Bankkonten passiert, evtl. müssen sie auf eine andere Bank transferiert werden, sonst verlieren alle Kunden ihr Geld.
```sql
CREATE TABLE IF NOT EXISTS Bank (  
	BankID INT PRIMARY KEY  
);
```
  
```sql
CREATE TABLE IF NOT EXISTS Bankkonto (  
	KontoID INT PRIMARY KEY,  
	BankID INT,  
	FOREIGN KEY (BankID)  
		  REFERENCES Bank(BankID)  
	ON DELETE NO ACTION  
);
```
  

### CASCADE

Wird zusammen mit ON DELETE oder ON UPDATE benutzt. Wenn der Parent gelöscht oder geupdatet wird, wird auch das Child gelöscht oder geupdatet. Eignet sich gut bei Muss-Beziehungen z.B. Gebäude und Räume. Wird das Gebäude gelöscht werden die Räume mit gelöscht.
```sql
CREATE TABLE IF NOT EXISTS Gebäude (  
GebäudeID INT PRIMARY KEY  
);
```
  
```sql
CREATE TABLE IF NOT EXISTS Raum (  
	RaumID INT PRIMARY KEY,  
	GebäudeID INT,  
	FOREIGN KEY (GebäudeID)  
			  REFERENCES Gebäude(GebäudeID)  
			  ON DELETE CASCADE  
);
```
  

#### SET NULL

Wenn der parent gelöscht wird, wird beim Child der Fremdschlüssel auf NULL gesetzt, das Tupel wird aber nicht gelöscht. Eignet sich gut bei starken Entitäten z.B. Mitarbeiter und Essenskarte. Wenn ein Mitarbeiter die Firma verlässt, soll die Essenskarte nicht gleich mitgelöscht werden.
```sql
CREATE TABLE IF NOT EXISTS Mitarbeiter (  
	MitarbeiterID INT PRIMARY KEY  
);
```
  
```sql
CREATE TABLE IF NOT EXISTS Essenskarte (  
	Kartennummer INT PRIMARY KEY,  
	MitarbeiterID INT,  
	FOREIGN KEY (MitarbeiterID)  
	REFERENCES Mitarbeiter(MitarbeiterID)  
	ON DELETE SET NULL  
);
```
  

#### SET DEFAULT

It is used in conjunction with ON DELETE or ON UPDATE. It means that the child data is set to their default values when the parent data is deleted or updated.

Wird zusammen mit ON DELETE oder ON UPDATE benutzt. Wenn der Parent gelöscht oder geupdatet wird, dann wird das Child auf einen vorher festgelegten default Wert gesetzt. WIr nehmen wieder das Beispiel von oben mit Mitarbeiter und Essenskarten. Hier haben wir den Vorteil, dass in unserer Tabelle keine NULL Werte stehen und dann können wir auch noch zusätzlich den Attributen NOT NULL zuweisen.
```sql
CREATE TABLE IF NOT EXISTS Mitarbeiter (  
	MitarbeiterID INT PRIMARY KEY  
);
```
  
```sql
CREATE TABLE IF NOT EXISTS Essenskarten (  
	Kartennummer INT PRIMARY KEY,  
	MitarbeiterID INT NOT NULL DEFAULT -1,  
	FOREIGN KEY (MitarbeiterID)  
	REFERENCES Mitarbeiter(MitarbeiterID)  
	ON DELETE SET DEFAULT  
);
```
  
  

  

## SQL befehle nach mathematischer Schreibweise
(nicht so wichtig)
Es werden hier nur die SQL Befehle und nicht die mathematische Schreibweise beschrieben

### Projektion:

Dabei werden nur einzelne Columns ausgewählt, indem man die Namen der Columns nach dem Select angibt.

Hier wird z.B: nur Vorname, Nachname und Geburtsdatum ausgegeben:
```sql
SELECT Vorname, Nachname, Geburtsdatum FROM Mitarbeiter;
```
  

Wenn man alle Columns will, muss man nicht alle Namen extra hinschreiben, sondern man kann einfach ein * schreiben:
```sql
SELECT * FROM Mitarbeiter;
```
  
  

### Selektion:

Dabei werden nur einzelne Tuples/Datensätze ausgewählt, die auf die entsprechende Bedingung zutreffen. Dafür benutzen wir den WHERE Befehl und die logischen Operatoren AND und OR.

Stellen wir uns vor, wir haben eine Mitarbeiterdatenbank und wollen nur diejenigen Mitarbeiter, die mehr als 1000 verdienen:
```sql
SELECT * FROM Mitarbeiter WHERE Gehalt > 1000;
```
  

Die Mitarbeiter, die mehr als 1000 aber weniger als 2000 verdienen:
```sql
SELECT * FROM Mitarbeiter WHERE Gehalt > 1000 AND Gehalt < 2000;
```
  

Die Mitarbeiter, die genau 1000 oder 2000 verdienen:
```sql
SELECT * FROM Mitarbeiter WHERE Gehalt = 1000 OR Gehalt = 2000;
```
  
  

Projektion und Selektion in Kombination:

Wir wollen nur die Nachnamen der Mitarbeiter, die mehr als 1000 verdienen, also kombinieren wir Projektion und Selektion:
```sql
SELECT Nachname FROM Mitarbeiter WHERE Gehalt > 1000;
```
  
  

### Vereinigung:

Dabei wollen wir zwei Tabellen, die das gleiche Relationsschema haben (also den gleichen Aufbau) zu einer Tabelle zusammenfassen.

Dafür benutzen wird den UNION Befehl.

Z.B. haben wir eine Datenbank Schüler und eine Datenbank Lehrer, beide haben die Columns Vorname, Nachname, Geburtsdatum.

Wir vereinigen mit:
```sql
SELECT * FROM Schüler UNION SELECT * FROM Lehrer;
```
 