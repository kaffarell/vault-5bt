Binomialverteilung
[Quelle 1](https://www.youtube.com/watch?v=UkOx8qdLAak)
[Quelle 2](https://www.youtube.com/watch?v=qRkUCU7oJ34)

Angenommen 20% der Lampen sind defekt und 20 Lampen werden als Stichprobe entnommen

Bernoulli Formel (Es gibt nur 2 Werte, entweder die Lampe funktioniert oder sie funktioniert nicht)

$P(E)={n \choose k} \cdot p^k \cdot q^{n-k}$

n ist die Gesamtanzahl der Versuche (20)
k ist die gesuchte anzahl (die defekten Lampen)
p ist die wahrscheinlichkeit für einen Treffer 
q ist die Gegenwahrscheinlichkeit (100 - p)

Wollen wir beispielsweise die Wahrscheinlichkeit für 8 defekte Lampen wissen so ist:
p = 0.2
q = 0.8
n = 20
k = 8 (wahrscheinlichkeit für 8 defekte lampen)
${n \choose k}$ ist dabei der Binomialkoeffizient
${20 \choose 8}$ in unserem Beispiel
Stellt man sich ein Wahrscheinlichkeitsbaumdiagramm vor, gibt diese an, bei wie vielen Wiederholungen (n) eine gewisse Sache (k) auftritt (=Alle Pfade bei denen eine Schraube defekt ist)
Berechnet wird diese durch $\frac{n!}{k!\cdot (n-k)!}$ (oder $nCr$ auf dem Taschenrechner $\rightarrow$ $n \; nCr \; k$ ) 

Die Binomialverteilung ist dabei die Wahrscheinlichkeit dass 1 Lampe kaputt ist, 2 Lampen Kaputt sind, 3 Lampen kaputt sind, ...
Die sieht in unserem Beispiel mit den Lampen so aus ![Binomial distribution](https://cdn.discordapp.com/attachments/613625981219110914/974348124938203256/unknown.png)

Wie man bereits in der oben stehenden Grafik erkennen kann ist die Wahrscheinlichkeit 4 Kaputte Lampen zu haben am höchsten. Dies wird als Erwartungswert bezeichnet.
Der Erwartungswert lässt sich wie folgt berechnen:
$E = n \cdot p$ (Wie oft etwas durchgeführt wird * die Wahrscheinlichkeit, dass etwas eintrifft)
In unserem Beispiel also $E=20\cdot 0.2 = 4$

Streuung S = sqrt(n * p * q)