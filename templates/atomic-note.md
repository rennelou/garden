---
id: thm-bolzano-weierstrass
type: theorem # theorem | definition | exercise
title: "Teorema de Bolzano-Weierstrass"
tags:
  - math/analysis
  - status/draft # draft | verified | leanified
created: 2026-07-22
course: "Análise Real I"
publish: true # Flag para o futuro blog exportar
lean_file: "lean/Analysis/BolzanoWeierstrass.lean"
---

# Teorema de Bolzano-Weierstrass

## ✍️ Manuscrito Original
> [!info] Documento de Origem
> ![[assets/handwritten/2026-07-22_bolzano.pdf#page=1]]
> *(Se o renderizador não suportar embed de PDF, link direto: [Ver PDF](assets/handwritten/2026-07-22_bolzano.pdf))*

---

## 📐 Formatação TeX (Gerado por LLM)

> [!theorem] Teorema (Bolzano-Weierstrass)
> Toda sequência limitada em $\mathbb{R}^n$ possui uma subsequência convergente.

### Demonstração
Seja $(x_k)_{k \in \mathbb{N}}$ uma sequência limitada em $\mathbb{R}^n$. Como $(x_k)$ é limitada, existe uma caixa $K = [a_1, b_1] \times \dots \times [a_n, b_n]$ tal que $x_k \in K$ para todo $k$.

Dividindo a caixa $K$ sucessivamente em $2^n$ sub-caixas idênticas...

---

## 🧩 Formalização em Lean 4

```lean
-- Importação da prova formal quando disponível
import Mathlib.Topology.Instances.Real

theorem bolzano_weierstrass {s : Set (EuclideanSpace ℝ (Fin n))} 
  (h1 : IsBounded s) (h2 : Set.Infinite s) : 
  ∃ x ∈ s, IsClusterPt x (Filter.principal s) := by
  sorry
