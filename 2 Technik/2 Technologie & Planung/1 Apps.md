# Android
## Klasse R
- R steht für Ressourcen
- Statische Klasse die zur kompilierzeit erstellt wird
- Hat viele statische variablen, die automatisch erstellt werden
- Mappt dateipfad zu resource zu einfachen attribut
	- Man muss also nicht im Code den Pfad zum (zB.:) Bild eingeben sondern man kann einfach `R.resources.name_der_datei` eingeben 

## Activities
- Enthalten Benutzeroberfläche
- Sind wie eine "Seite"
- Haben ein eigenes Fenster (Vollbild oder nicht)

## Services
- Komponent wie Activity, aber ohne Benutzeroberfläche
- Läuft im Hintergrund der App

## Intents
- Mit Intents können activities nachrichten zu anderen activities schicken
- Mit einem Intent kann zum beispiel eine andere activitity aufgehen

## Fragment
- Ist ein Teil einer Activity (Teil einer Benutzeroberfläche)
- Zum Beispiel inputfeld mit button -> kann dann als fragment wieder benützt werden
- Brauchte es weil man nicht eine Activity für Tablet und eine für Handy machen kann (gleiche funktionen etc. aber anderes layout)

## Broadcast Receiver
- Reagieren auf systemweite nachrichten
- Zum beispiel reagiert ein broadcast receiver auf der nachricht "Batteriestand ist niedrich"

# Nicht Native Apps
- Beispiele:
	- Flutter
	- React Native
	- Native Script
	- Ionic
	
- Mann programmiert mit Javascript (oder bei Flutter mit Dart), HTML und CSS. Man kann so schneller User-Interfaces erstellen, wie bei Webseiten(Mann kann auch code einer webapp wiederverwenden für einer app). Nachteil ist dass diese Apps meistents längsamer laufen und auch nur begrenzt auf nativen ressourcen zugreifen können (Kamera, Sensoren, etc).