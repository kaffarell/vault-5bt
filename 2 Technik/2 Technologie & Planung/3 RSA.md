# RSA

Der RSA Algorithmus wird verwendet um privaten und öffentlichen Schlüssel für die asymmetrische Verschlüsselung zu erstellen.
Die Sicherheit des RSA beruht auf dem modulo Operator und auf dem Faktorisierungsproblem, das bedeutet, dass es unmöglich ist, die Faktoren einer sehr großen Zahl zu finden, wenn die beiden Faktoren große Primzahlen sind.

Folgende Schritte müssen durchgeführt werden:

- zwei Primzahlen p und q werden gewählt (in der Praxis müssen diese extrem groß sein, um die Sicherheit zu gewährleisten, in unserem Beispiel nehmen wir kleine Zahlen)
  > p = 11  q = 17
- beide Primzahlen werden miteinander multipliziert und ergeben N
  > N = p * q = 11 * 17 = 187
- beide Primzahlen minus 1 werden miteinander multipliziert und ergeben Φ(n)
  > Φ(N) = (p-1) * (q-1) = (11-1) * (17-1) = 10 * 16 = 160
- es muss eine Zahl e gefunden werden für die gilt 1 < e < Φ(N) und e und Φ(N) sind teilerfremd.
  Am einfachsten ist das, in dem man eine Primzahl wählt, die kleiner als Φ(N) ist und nicht ein Teiler von Φ(N) ist.
  > e = 23, weil e ist größer als 1 und kleiner als 160 und 160 mod 23 ist nicht 0.
- Der öffentliche Schlüssel ist jetzt fertig. N und e können veröffentlicht werden
- Jetzt muss noch der private Schlüssel berechnet werden, dafür verwenden wir den erweiterten euklidischen Algorithmus
  Das ist der komplizierteste Teil der Berechnung. Am einfachsten die Berechnung in Tabellen/Matrix schreibweise
  
  Wir erstellen folgende Tabelle:
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |      |   |   |   |   |
  
 
  Wir tragen unsere Werte für Φ(N) und e ein. R, x und d ignorieren wir für den Moment:
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23|   |   |   |
  
 
  Jetzt schauen wir wie oft e in Φ(N) platz hat, also floor(160 / 23) = floor(6.96) = 6
  Das tragen wir in der R Spalte ein.
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23| 6 |   |   |
  

  Dann schauen wir wie viel Rest bleibt, also 160 mod 23 = 22.
  Das tragen wir in der nächsten Zeile unter dem e ein.
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23| 6 |   |   |
  |      | 22|   |   |   |
  
       
  Das alte e, in dem Fall 23, schreiben wir in die neue Φ(N) Spalte
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23| 6 |   |   |
  |   23 | 22|   |   |   |
  
    
  Diese Schritte wiederholen wir jetzt so lange, bis die Division aufgeht, also modulo 0 rauskommt:
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23| 6 |   |   |
  |   23 | 22| 1 |   |   |
  |   22 |  1| 22|   |   |
  |   1  |  0|   |   |   |
  
    
  Jetzt müssen x und d berechnet werden! Man rechnet die Tabelle von unten nach oben.
  Zuerst wir 1 und 0 hinübergeschrieben
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23| 6 |   |   |
  |   23 | 22| 1 |   |   |
  |   22 |  1| 22|   |   |
  |   1  |  0|   | 1 | 0 | 
  
    
  Das Ergebnis von d wir das x der Zeile darober:
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23| 6 |   |   |
  |   23 | 22| 1 |   |   |
  |   22 |  1| 22| 0 |   |
  |   1  |  0|   | 1 | 0 |
  
    
  Das d dieser Zeile wird jetzt berchnet, in dem man folgende Gleichung löst:  
  > 1 = Φ(N) * x + e * d  
  Wir setzen die Werte dieser Zeile ein und lösen die Gleichung:  
  > 1 = 22 * 0 + 1 * d  
  > 1 = 1*d  
  > 1 = d  
  
  Das Ergebnis schreiben wir dann in die d Spalte und auch wieder in die darüberliegende Zeile in die x Spalte:
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23| 6 |   |   |
  |   23 | 22| 1 | 1 |   |
  |   22 |  1| 22| 0 | 1 |
  |   1  |  0|   | 1 | 0 |
  
  
  Jetzt müssen wir wieder die Gleichung lösen:
  > 1 = Φ(N) * x + e * d  
  Wir setzen wieder die Werte dieser Zeile ein und lösen:
  > 1 = 23 * 1 + 22 * d  
  > 1 = 23 + 22d  
  > -22 = 22d  
  > -1 = d  
  
  Wir tragen die Ergebnisse ein:
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23| 6 |-1 |   |
  |   23 | 22| 1 | 1 | -1|
  |   22 |  1| 22| 0 | 1 |
  |   1  |  0|   | 1 | 0 |
  
    
  Diesen Prozess wiederholen wir bis ganz oben. In unserem Beispiel braucht es nur noch eine Berechnung deshalb zeige ich sie vollständigzeithalber:
  > 1 = Φ(N) * x + e * d  
  > 1 = 160 * -1 + 23 * d  
  > 1 = -160 + 23d  
  > 161 = 23d  
  > 7 = d  
  
  Hinweis: Für d muss in jedem Schritt eine Ganzzahl herauskommen, ansonsten ist ein Rechenfehler vorgekommen
  
  Wir tragen das Ergebnis ein:
  
  | Φ(N) | e | R | x | d |
  | ---- | - | - | - | - |
  |  160 | 23| 6 |-1 | 7 |
  |   23 | 22| 1 | 1 | -1|
  |   22 |  1| 22| 0 | 1 |
  |   1  |  0|   | 1 | 0 |
  
    
  Unser letztes Ergebnis für d ist 7, das ist also unser privater Schlüssel, den wir auf keinen Fall veröffentlichen dürfen.
  WICHTIG: Falls d negativ wäre, was durchaus vorkommen kann, dann muss noch einmal Φ(N) addiert werden. In diesem Fall müsste also 160 addiert werden, wenn d negativ wäre.
  
  
  ## Die eigentliche Verschlüsselung
  
  Jetzt, nachdem öffentlicher und privater Schlüssel berechnet wurden, kann jede Zahl kleiner als N verschlüsselt werden.
  Dafür bracuht es folgende Formel:
  > z^e % N  
  dabei ist z eine Zahl < N und e und N unser öffentlicher Schlüssel.  
  Zum Beispiel verschlüsseln wir jetzt die Zahl 50.
  > 50^23 mod 187 = 84
  
  Die Zahl 84 können wir jetzt dem Empfänger problemlos schicken, da sie nur mit dem privaten Schlüssel d wieder entschlüsselt werden kann.
  Dafür benutzen wir folgende Formel
  > c^d % N  
  dabei ist c die verschlüsselte Zahl, d der private Key und N der Teil des öffentlichen Schlüssels.  
  Wir setzen ein:
  > 84^7 mod 187 = 50
  
  Wir erhalten wieder 50, also die Zahl, die verschlüsselt wurde, also hat alles perfekt funktioniert!
  
  Finally :))
