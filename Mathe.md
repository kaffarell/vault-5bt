#### Abeltiungsregeln:
```ad-success
title: Einfache Regeln
$(e^x)'=e^x$
$x'=1$ 
$k'=0$ 
$(x^n)' = n \cdot x^{n/1}$ 
$\ln(x)' = \frac{1}{x}$
```

```ad-success
title: Komplexere Regeln
$(sin(x)' = cos(x)$ **|** $cos(x)' = -sin(x)$

$(f(x) * g(x))' = f(x)' * g(x) + g(x)' * f(x)$

$(f(x) \pm g(x))' = f(x)' \pm g(x)'$ **|** $(c*f(x))' = c * f(x)'$

$\left(\frac{f(x)}{g(x)}\right)' = \frac{f(x)' * g(x) - f(x) * g(x)'}{g(x)^2}$

$\left(e^{\ln(x)}\right)' = e^{\ln(x)} \cdot \ln(x)' = x \cdot \ln(x)' = 1$
```
---
#### Integration:
```ad-success
title: Regeln

$\int x^n dx = \frac{x^{n+1}}{n+1} + C$

$\int 1\;dx = x + C$

$\int 1 + 2x\;dx = \int 1\;dx + \int 2x\;dx = x + x^2 + C$

$\int \frac{1}{x} dx = \int x^{-1} dx = ln(x) + c$
```

```ad-success
title: Substitution
$\int \frac{e^x}{1+e^x} dx$
$u = 1+e^x$
$u' = e^x \rightarrow dx = \frac{du}{e^x}$
```

```ad-success
title: Partielles integrieren
$\int f(x)' \cdot g(x) = f(x) \cdot g(x) - \int f(x) \cdot g(x)'$
```

```ad-question
title: Partialbruchzerlegung

```

```ad-success
title: Länge einer Kurve
$\int_{x_1}^{x_2} \sqrt[2]{1+y'^{2}} \; dx$
```
---
##### Rotationskörper
```ad-success
title: Mantel
$2\pi \int_{a}^{b} y \cdot \sqrt[2]{1+y'^2} \; dx$
```

```ad-success
title: Volumen
$\pi \cdot \int_{a}^{b} f(x)^2 \;dx$
```

```ad-success
title: Periodischer Mittelwert
$\frac{1}{T} \cdot \int_{0}^{T} f(t) \;dx$
```
```ad-success
title: Nicht periodischer Mittelwert
$\frac{1}{x_2 - x_1} \cdot \int_{x_1}^{x_2} f(t) \;dx$
```
---
#### Differenzialgleichung
```ad-success
title: Trennung der Variablen
Schirtt | Erklärung
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
```





