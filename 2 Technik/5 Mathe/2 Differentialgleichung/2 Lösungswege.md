#### Lösungswege
```ad-success
title: Trennung der Variablen
Schritt | Erklärung
--------|------------
$y' - 3x^2 \cdot y = 0$ | Gegebene Differenzialgleichung
$\downarrow$ | auf y' umstellen
$y' = 3x^2 \cdot y$ |
$\downarrow$ | y' zu $\frac{d_y}{d_x}$ umschreiben
$\frac{d_y}{d_x}=3x^2 \cdot y$ |
$\downarrow$ | y' & $d_y$ auf eine Seite und x und $d_x$ auf die andere Seite geben 
$\frac{1}{y}\;dy=3x^2\;dx$ |
$\downarrow$ | Beide seiten integrieren
$\ln(\|y\|) = \frac{3x^3}{3} + C$ | +C nur auf einer Seite, weil man dass C von links subtrahieren und rechts zu einem neuen C machen kann
$\downarrow$ | e^ rechnen um $\ln$ aufzulösen 
$\|y\|= e^{x^3}$ |
$\downarrow$ | $\cdot\;C_0$ rechnen um $\|y\|$ aufzulösen
$y = e^{x^3} \cdot C_0$ |
```

```ad-success
title: Spezieller Lösungsansatz
$y'+2\cdot y=4x-5$
↳ 4x-5 ist die Störfunktion

Aus Tabelle (verlinken) Lösungsansatz für gegebene Störfunktion entnehmen

$y_p = A \cdot x + B$ 
↳ Funktion ableiten $\rightarrow$ $y_p' = A$


$y_p$ und $y_p'$ in die Originale Formel einsetzen
$\downarrow$
$y' + 2 \cdot y = 4x - 5$
$A+2 \cdot (A\cdot x+B)=4x-5$
$A+2A\cdot x+2B = 4x-5$
$\downarrow$ Koeffizientenvergleich
$\textcolor{red}{2A}\cdot x+(\textcolor{purple}{A+2B})=\textcolor{red}{4}\cdot x+(\textcolor{purple}{-5})$
$\downarrow$
$x^1:\;\;\;\textcolor{red}{2A}=\textcolor{red}{4}$
$x^0:\;\;\;\textcolor{purple}{A+2B}=\textcolor{purple}{-5}$
$\downarrow$
$A=2;\;\;B=-3.5$
↳ $y_p = 2x-3.5$

Alle Lösungsanstätze stehen unten:
![Ansatz](https://cdn.discordapp.com/attachments/875185482928103444/974311439558905896/unknown.png)
```

```ad-success
title: Variation der Konstanten
$y'-2x\cdot y = e^{x^2}$

Homogene Lösung finden, indem man die Differentialgleichung 0 setzt
($y_h = C \cdot e^{x^2}$)

$C$ der homogen Lösung zu Funktion umwandeln
$\downarrow$
$y_p = C(x) \cdot e^{x^2}$
$\downarrow$ Ableitung Bilden
$y_p' = C'(x) \cdot e^{x^2} + C(x) \cdot 2x \cdot e^{x^2}$

$y_p$ und $y_p'$ in Originale Aufgabenstellung einsetzen
$C'(x)\cdot e^{x^2} + 2x \cdot C(x) \cdot e^{x^2} - 2x \cdot C(x) \cdot e^{x^2} = e^{x^2}$
|
$\downarrow$ $C(x)$ streicht sich weg und $C(x)'$ bleibt übrig
$C(x)' \cdot e^{x^2} = e^{x^2}$
$C(x)' = 1$
$C(x)=\int 1 \; dx = x$
Lösung von $C(x)$ in $y_p$ einsetzen
$y_p=x\cdot e^{x^2}$
```
