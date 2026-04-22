# Exercícios do Professor Felipe — P, NP e co-NP

**Disciplina:** Fundamentos de Projeto e Análise de Algoritmos · PUC Minas  
**Professor:** Felipe de Castro Belém  

---

> **Enunciado:** Verifique se os problemas abaixo pertencem à classe P, NP e/ou co-NP. Forneça o problema de decisão correspondente (certificado positivo e negativo). Explique seu raciocínio.

---

### Exercício 1
Encontrar o maior valor de um vetor.

### Exercício 2
Avaliar se um dado número é primo.

### Exercício 3
Ordenar um vetor de maneira crescente.

### Exercício 4
Avaliar se um grafo é hamiltoniano.

### Exercício 5
Avaliar se um grafo é euleriano.

### Exercício 6
Encontrar uma árvore geradora de um grafo.

### Exercício 7
Verificar se um grafo é 3-colorável.

### Exercício 8
Verificar se um grafo é 2-colorável.

### Exercício 9
Encontrar o maior subgrafo completo (i.e., clique) de um grafo.

### Exercício 10
Encontrar o conjunto independente máximo de um grafo.

### Exercício 11
Encontrar a cobertura mínima de vértices de um grafo.

### Exercício 12
Encontrar a cobertura mínima de arestas de um grafo.

### Exercício 13
Contar a quantidade de subconjuntos existentes em um conjunto qualquer.

---
---
---

# GABARITO

---

### Gabarito 1 — Maior valor de um vetor

**Problema de decisão:** "Dado vetor V de n elementos e valor k, o maior valor de V é ≥ k?"

**Resolução:** Percorrer o vetor uma vez → O(n) → polinomial.

**Certificado +:** Índice i com V[i] ≥ k e V[i] = max. Verificação: percorrer e confirmar → O(n).  
**Certificado −:** Percorrer e verificar que todos < k → O(n).

**Classe: P, NP e co-NP.**

---

### Gabarito 2 — Número primo

**Problema de decisão:** "Dado inteiro n, n é primo?"

**Resolução:** Teste AKS (2002) → tempo polinomial → P.

**Certificado +:** Certificado de Pratt, ou certificado vazio (já que está em P).  
**Certificado −:** Divisor d com 1 < d < n e d | n → verificação O(log² n).

**Classe: P, NP e co-NP.**

---

### Gabarito 3 — Ordenar vetor

**Problema de decisão:** "Dado vetor V, existe permutação ordenada?" (trivialmente SIM). Versão útil: "V já está ordenado?"

**Resolução:** Merge Sort O(n log n) → polinomial.

**Certificado +:** Vetor ordenado → checar V[i] ≤ V[i+1] → O(n).  
**Certificado −:** Par (i, i+1) com V[i] > V[i+1] → O(1).

**Classe: P, NP e co-NP.**

---

### Gabarito 4 — Grafo hamiltoniano

**Problema de decisão:** "Dado grafo G, existe ciclo que passe por todos os vértices exatamente uma vez?"

**Resolução:** Sem algoritmo polinomial conhecido. NP-Completo (Karp, 1972).

**Certificado +:** Sequência de vértices do ciclo → checar unicidade + arestas → O(V).  
**Certificado −:** Não se conhece certificado polinomial genérico.

**Classe: NP e NP-Completo. Não se sabe se está em P ou co-NP.**

---

### Gabarito 5 — Grafo euleriano

**Problema de decisão:** "Dado grafo conexo G, existe circuito que percorra todas as arestas exatamente uma vez?"

**Resolução:** Teorema de Euler → existe ⟺ conexo + todos os vértices com grau par → O(V + E).

**Certificado +:** Sequência de arestas do circuito → checar cada aresta uma vez → O(E).  
**Certificado −:** Vértice com grau ímpar → O(grau).

**Classe: P, NP e co-NP.**

> ⚠️ Euler (arestas) → P. Hamilton (vértices) → NP-Completo.

---

### Gabarito 6 — Árvore geradora

**Problema de decisão:** "Dado grafo G, existe árvore geradora?" (= "G é conexo?")

**Resolução:** BFS/DFS → O(V + E). Kruskal/Prim → polinomial.

**Certificado +:** A árvore (V-1 arestas) → verificar conexidade e aciclo → O(V + E).  
**Certificado −:** Dois vértices u, v sem caminho → BFS de u, v não alcançado → O(V + E).

**Classe: P, NP e co-NP.**

---

### Gabarito 7 — 3-coloração

**Problema de decisão:** "Dado grafo G, é possível colorir vértices com ≤ 3 cores sem adjacentes iguais?"

**Resolução:** NP-Completo (redução de 3-SAT).

**Certificado +:** Atribuição de cores → checar cada aresta cor(u) ≠ cor(v) → O(E).  
**Certificado −:** Não se conhece certificado polinomial genérico.

**Classe: NP e NP-Completo. Não se sabe se está em P ou co-NP.**

---

### Gabarito 8 — 2-coloração

**Problema de decisão:** "Dado grafo G, é possível colorir com 2 cores sem adjacentes iguais?"

**Resolução:** 2-colorável ⟺ bipartido ⟺ sem ciclos ímpares → BFS/DFS → O(V + E).

**Certificado +:** Atribuição de 2 cores → checar cada aresta → O(E).  
**Certificado −:** Ciclo de comprimento ímpar → percorrer e confirmar → O(V).

**Classe: P, NP e co-NP.**

> ⚠️ 2-coloração → P. 3-coloração → NP-Completo.

---

### Gabarito 9 — Maior clique

**Problema de decisão:** "Dado grafo G e inteiro k, existe clique de tamanho ≥ k?"

**Resolução:** NP-Completo (21 problemas de Karp).

**Certificado +:** Conjunto de k vértices → checar todos os pares adjacentes → O(k²).  
**Certificado −:** Não se conhece certificado polinomial genérico.

**Classe: NP e NP-Completo. Não se sabe se está em P ou co-NP.**

---

### Gabarito 10 — Conjunto independente máximo

**Problema de decisão:** "Dado grafo G e inteiro k, existe conjunto independente de tamanho ≥ k?"

**Resolução:** NP-Completo. Complemento da clique: independente em G = clique em Ḡ.

**Certificado +:** Conjunto de k vértices → checar nenhum par adjacente → O(k²).  
**Certificado −:** Não se conhece certificado polinomial genérico.

**Classe: NP e NP-Completo. Não se sabe se está em P ou co-NP.**

---

### Gabarito 11 — Cobertura mínima de vértices

**Problema de decisão:** "Dado grafo G e inteiro k, existe cobertura de vértices de tamanho ≤ k?"

**Resolução:** NP-Completo (Karp). C é cobertura ⟺ V \ C é conjunto independente.

**Certificado +:** Conjunto de ≤ k vértices → para cada aresta (u,v), checar u ∈ C ou v ∈ C → O(E).  
**Certificado −:** Não se conhece certificado polinomial genérico.

**Classe: NP e NP-Completo. Não se sabe se está em P ou co-NP.**

---

### Gabarito 12 — Cobertura mínima de arestas

**Problema de decisão:** "Dado grafo G sem vértices isolados e inteiro k, existe cobertura de arestas de tamanho ≤ k?"

**Resolução:** Existe algoritmo polinomial! Emparelhamento máximo (Edmonds, O(V³)) + extensão gulosa.

**Certificado +:** Conjunto de ≤ k arestas → checar todo vértice incidente → O(V + k).  
**Certificado −:** Como está em P, rodar o algoritmo basta.

**Classe: P, NP e co-NP.**

> ⚠️ Cobertura de **vértices** → NP-Completo. Cobertura de **arestas** → P.

---

### Gabarito 13 — Contar subconjuntos

**Problema de decisão:** "Dado conjunto S de n elementos, quantidade de subconjuntos ≥ k?"

**Resolução:** Sempre 2^n subconjuntos. Calcular 2^n → O(n). Comparar com k → O(1). Polinomial.

**Certificado +:** Valor 2^n → calcular e confirmar ≥ k → O(n).  
**Certificado −:** Valor 2^n → calcular e confirmar < k → O(n).

**Classe: P, NP e co-NP.**

**Atenção:** *Contar* → P. *Listar* todos os 2^n → exponencial (output exponencial).

---

## Tabela Resumo

| # | Problema | P? | NP? | co-NP? | NP-C? |
|---|----------|----|-----|--------|-------|
| 1 | Maior valor do vetor | ✅ | ✅ | ✅ | ❌ |
| 2 | Número primo | ✅ | ✅ | ✅ | ❌ |
| 3 | Ordenar vetor | ✅ | ✅ | ✅ | ❌ |
| 4 | Grafo hamiltoniano | ❓ | ✅ | ❓ | ✅ |
| 5 | Grafo euleriano | ✅ | ✅ | ✅ | ❌ |
| 6 | Árvore geradora | ✅ | ✅ | ✅ | ❌ |
| 7 | 3-coloração | ❓ | ✅ | ❓ | ✅ |
| 8 | 2-coloração | ✅ | ✅ | ✅ | ❌ |
| 9 | Maior clique | ❓ | ✅ | ❓ | ✅ |
| 10 | Conjunto independ. máx. | ❓ | ✅ | ❓ | ✅ |
| 11 | Cobertura mín. vértices | ❓ | ✅ | ❓ | ✅ |
| 12 | Cobertura mín. arestas | ✅ | ✅ | ✅ | ❌ |
| 13 | Contar subconjuntos | ✅ | ✅ | ✅ | ❌ |

**Legenda:** ✅ = sim · ❓ = não se sabe (depende de P=NP) · ❌ = não
