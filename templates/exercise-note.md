---
id: ex-lista1-q3-analise
type: exercise # options: exercise | problem
title: "Lista 1 - Q3: Convergência da Média de Cesàro"
course: "Análise Real I"
source: "Lista 1 / Impa / Prof. X"
tags:
  - math/analysis/sequences
  - status/verified
created: 2026-07-22
publish: true
lean_file: "lean/Exercises/CesaroMean.lean"
---

# Exercício: Média de Cesàro

## ✍️ Manuscrito Original
> [!info] Documento de Origem
> ![[assets/handwritten/2026-07-22_lista1_q3.pdf]]

---

## 📐 Enunciado & Solução (LaTeX)

> [!question] Enunciado
> Seja $(a_n)$ uma sequência de números reais tal que $a_n \to a$. Prove que a sequência de médias de Cesàro $c_n = \frac{1}{n}\sum_{k=1}^n a_k$ também converge para $a$.

### Solução
Dado $\varepsilon > 0$, como $a_n \to a$, existe $N_1 \in \mathbb{N}$ tal que para todo $n > N_1$, $|a_n - a| < \frac{\varepsilon}{2}$.

Escrevendo $c_n - a = \frac{1}{n}\sum_{k=1}^n (a_k - a)$, dividimos a soma em duas partes...

$$\begin{aligned}
|c_n - a| &\le \frac{1}{n}\sum_{k=1}^{N_1} |a_k - a| + \frac{1}{n}\sum_{k=N_1+1}^n |a_k - a| \\
&< \frac{M}{n} + \frac{(n - N_1)}{n}\frac{\varepsilon}{2}
\end{aligned}$$

---

## 🔗 Referências & Mapeamento
* **Aplica o teorema:** [[thm-limite-sequencias]]
* **Utilizado em:** [[ex-prova1-q1]]
