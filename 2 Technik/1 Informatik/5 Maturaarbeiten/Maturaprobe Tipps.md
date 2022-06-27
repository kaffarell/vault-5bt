## ER-Modellierung
* Keine schwache Entitäten oder Generalisierung reinzwingen (braucht es meistens nicht)
* Bei der Beziehung nur verben rein schreiben
* Unklarheiten ob 1:n oder n:m (Manchmal schwierig zu erkennen, evtl. Tabelle machen)
* **Wichtig: chen-notation und min:max notation nicht vermischen!**
* Entität sollte man nur erstellen wenn es mehr als ein String ist (sonst einfach attribut)
* **Wichtig: keine Fremdschlüssel im ER-Diagramm (also sind nur partielle Schlüssel gestrichelt unterstrichen)**
* **Wichtig: Entweder alle Primärschlüssel unterstreichen oder keine!**
* Redundante Attribute vermeiden (zB.: Alter und Geburtsdatum in Tabelle)
	* Wenn man zB.: Alter nicht berechnen will und man braucht es oft, dann kann es trotzdem drinnen sein (sollte in der Beschreibung erklärt sein)

### Schwache Entität
* Schreibweise mit doppelt umrandeter Raute
* Richtung mit pfeil oder mit zwei Verbindungslinien
* Wenn es eine Entität ohne der anderen nicht geben kann
* Wenn (bei der min:max notation) eine Beziehung mit 1/1 gibt, ist eine schwache entität möglich
* Zum Beispiel ist eine Speisekarte ohne Speisen trotzdem möglich -> muss nicht schwache Entität sein

## Logisches Schema
* n:m Beziehungen haben immer zwischentabellen (Zwischentabellen haben die zwei primary keys auch als foreign keys)
* Ternäre Beziehunge meiden (oder gut aufpassen) (man kann viel falsch machen)
* Kreise sollte man auch vermeiden
  
## Generell  
* Bei einer Sprache bleiben (entweder Deutsch oder Englisch)
* Entweder Plural oder Singular, egal welches aber konstant bei einem bleiben


## Programmierung
* Unterschied sum und count
* avg() nur von listen und nicht von einziger zahl machen (also verschachtelte selects benützen)
* Platzhalter bei SQL-Abfragen (_ oder %)
* Jede Subquery hat ein alias
* Datumformat richtig nutzen
	* Wie das datum als string geschrieben wird
	* Date speichert datum
	* Datetime speichert datum mit zeit
	* Timestamp -> aktuelle zeit