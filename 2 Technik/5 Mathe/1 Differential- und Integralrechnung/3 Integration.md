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
---
##### Mittelwert
```ad-success
title: Periodischer Mittelwert
$\frac{1}{T} \cdot \int_{0}^{T} f(t) \;dx$
```
```ad-success
title: Nicht periodischer Mittelwert
$\frac{1}{x_2 - x_1} \cdot \int_{x_1}^{x_2} f(t) \;dx$
```