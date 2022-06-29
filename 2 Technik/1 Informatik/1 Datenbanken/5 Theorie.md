## Normalformen:
#### Erste Normalform:
Wenn alle Informationen einer Tabelle Atomar vorliegen
![[1NF.png]]

#### Zweite Normalform:
Wenn jedes Nichtschlüsselattribut von jedem Schlüsselkandidaten [voll funktional](https://www.datenbanken-verstehen.de/datenmodellierung/normalisierung/abhaengigkeiten-normalisierung/ "Abhängigkeiten") abhängig ist. Jedes nicht-primäre Attribut (nicht Teil eines Schlüssels) ist jeweils von allen ganzen Schlüsseln abhängig, nicht nur von einem Teil eines Schlüssels.
![[2NF.png]]

#### Dritte Normalform:
Wenn kein Nichtschlüsselattribut [transitiv](https://www.datenbanken-verstehen.de/datenmodellierung/normalisierung/abhaengigkeiten-normalisierung/ "Abhängigkeiten") von einem Kandidatenschlüssel abhängt. Die dritte Normalform ist erreicht, wenn sich das Relationenschema in 2NF befindet, und kein Nichtschlüsselattribut (hellgraue Zellen in der Tabelle) von einem anderen Nichtschlüsselattribut funktional abhängig ist.
![[3NF.png]]

## Synthesealgorithmus
#### Theorie
Der Synthesealgorithmus dient dazu ein Relationenschema in die dritte Normalform zu bringen.

#### Linksreduktion
Bei der Linksreduktion versucht man Attribute auf der Linken Seite zu streichen. Dies wird erreicht indem alle Relationen der Reihe nach durch gegangen werden und man versucht Links Attribute zu streichen, welche in der Transitiven Hülle bereits vorhanden sind. Links darf immer nur **EIN** Element entfernt werden und es darf nicht leer stehen.

Beispiel: A,B,C,D,E,F
-  ${\displaystyle A\rightarrow B,E}$
-  ${\displaystyle A{\underline {E}}\rightarrow B,D}$
-  ${\displaystyle F\rightarrow C,D}$
-  ${\displaystyle CD\rightarrow B,E,F}$
-  ${\displaystyle {\underline {C}}F\rightarrow B}$

E fällt weg, da es sich bereits in der transitiven Hülle von $A^+$ befindet.
In der letyten Relation fällt C weg, da sich C bereits in der transitiven Hülle von $F^+$ befindet.

#### Rechtsreduktion

#### Leere Klauseln
#### Zusammenfassen

## ACID
Atomicity (Jede "Transaktion" muss in einem mal ausgeführt werden)
Consistency (Datenbank wird nur in validem Zustand hinterlassen)
Isolation (Transaktionen geschehen unabhängig von einander und ohne sich gegenseitig zu beinflussen)
Durability (Die Änderungen einer Erflogreichen Transaktion bleiben vorhanden, sogar wenn das System aufällt)