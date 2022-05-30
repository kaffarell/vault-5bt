```ad-success
title: Partialbruchzerlegung
Schritt | Erklärung
--------|------------
$\int-\frac{15}{x^2+3x-4}\;dx$|Gegebene Aufgabenstellung
$\downarrow$|
$x^2+3x-4=0$|Nenner 0 setzen und $x_1$ & $x_2$ ausrechnen
$x_1 = 1$|
$x_2 = -4$|
$\downarrow$|
$\int \frac{A}{x-x_1} + \frac{B}{x-x_2}\;dx$|
$\int \frac{A}{x-1} + \frac{B}{x+4}\;dx$|In unserem Beispiel
$\downarrow$|Bruch auf gemeinsamen Nenner bringen
$\int \frac{A \cdot (x+4) + B \cdot (x-1)}{(x-1)\cdot (x+4)}\;dx$|
$\downarrow$|
$\int \frac{A \cdot (x+4) + B \cdot (x-1)}{(x-1)\cdot (x+4)}\;dx = \int-\frac{15}{x^2+3x-4}\;dx$ |Mit Originaler gleich setzen
$\downarrow$|Zähler vom Bruch ausrechnen und Gleichungssystem lösen
$5B = -15$|
$B=-3$|
$-5A=-15$|
$A=3$|
$\downarrow$|
$\int \frac{3}{x+4} - \frac{3}{x+1}\;dx$|A & B einsetzen
$\int \frac{3}{x+4} \;dx - \int \frac{3}{x+1}\;dx$|Integral mittels $\int \frac{1}{x}\;dx=\ln(x)$ $\rightarrow \int \frac{1}{x+4}\;dx=\ln(x+4)$ lösen
$3\cdot \ln(x+4) - 3\cdot \ln(x+1)$|
```
