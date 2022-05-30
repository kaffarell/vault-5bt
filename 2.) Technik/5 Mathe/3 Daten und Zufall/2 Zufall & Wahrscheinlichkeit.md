Baumdiagramm
![Uebung](https://cdn.discordapp.com/attachments/806161662380867604/974364483566858260/unknown.png)

```nomnoml
[.] -> [A (15%)]
[.] -> [B (35%)]
[.] -> [C (50%)]

[A (15%)] -> [Def (8%)]
[A (15%)] -> [OK (92%)]

[B (35%)] -> [Def (20%)]
[B (35%)] -> [OK (80%)]

[C (50%)] -> [Def (7%)]
[C (50%)] -> [OK (93%)]
```
1.i) Unbrauchbar (Defekt)
	$0.15\cdot 0.08+0.35\cdot 0.2+0.5\cdot0.07=0.117\cdot 100=11.7\%$

1.ii) In Ordnung ist (OK)
	$0.15\cdot 0.92+0.35\cdot 0.8+0.5\cdot0.91=0.873\cdot 100=87.3\%$

1.iii) Von A stammt und unbrauchbar ist
	$0.15\cdot 0.08=1.2\%$

1.iv) Von A stammt wenn er unbrauchbar ist
	Defekte A = $0.15 \cdot 0.08 = 0.012$
	Defekte B = $0.35 \cdot 0.20 = 0.07$
	Defekte C = $0.50 \cdot 0.07 = 0.035$
	Alle Defekten Möglichkeiten Addieren = $0.117$ 
	Defekte von A durch alle Defekten möglichkeiten Teilen
	$\frac{1.2\%}{11.7\%} = 0.102 = 10.2\%$

