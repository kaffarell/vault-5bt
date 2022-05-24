- __Trigger__ für Mitfahrgelegenheitanmeldeschluss
	- gleich bei Fahrtbeginn--> Boolean auf false setzen
	- eine Woche nach Fahrtbeginn --> aus der Datenbank löschen

- Überprüfen ob Führerschein gültig --> wenn der Fahrer eine neue Fahrt erstellen will --> Clientseitig


# Abfragen
SELECT Vorname, Nachname, StartOrt, ZielOrt, Startzeit, Ankunftszeit, Kostenbeitrag, Fahrtzeit, Gepäck, Tiere
FROM Mitfahrgelegenheit
JOIN Fahrer using(FahrerID)
HAVING Startzeit >= NOW
AND
HAVING Vormerkungsstatus;