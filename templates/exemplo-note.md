---
id: eg-funcao-weierstrass
type: example # options: example | counterexample
title: "Função de Weierstrass (Contínua e Nãodiferenciável)"
course: "Análise Real"
tags:
  - math/analysis/counterexamples
  - status/draft
created: 2026-07-22
publish: true
lean_file: "lean/Examples/WeierstrassFunction.lean"
---

# Exemplo: Função de Weierstrass

## ✍️ Manuscrito Original
> [!info] Documento de Origem
> ![[assets/handwritten/2026-07-22_weierstrass_eg.pdf]]

---

## 📐 Enunciado & Construção (LaTeX)

> [!example] Função de Weierstrass
> Exemplo de função $f: \mathbb{R} \to \mathbb{R}$ que é contínua em todos os pontos, mas não é diferenciável em nenhum ponto.

### Definição
$$f(x) = \sum_{n=0}^{\infty} a^n \cos(b^n \pi x)$$
onde $0 < a < 1$, $b$ é um inteiro ímpar ímpar e $ab > 1 + \frac{3}{2}\pi$.

### Propriedades Ilustradas
* Mostra que a intuição de "continuidade implica diferenciabilidade quase em toda parte" é falsa.
* Serve de contraexemplo para convergência uniforme de derivadas.

---

## 🔗 Referências & Mapeamento
* **Ilustra a definição:** [[def-continuidade]], [[def-diferenciabilidade]]
* **Relacionado ao teorema:** [[thm-convergencia-uniforme-derivadas]]
