# Exercícios do Professor Felipe — P, NP e co-NP

**Disciplina:** Fundamentos de Projeto e Análise de Algoritmos · PUC Minas  
**Professor:** Felipe de Castro Belém  

---

## Tabela de Algoritmos — O que cada um resolve

| Algoritmo | O que resolve | Complexidade |
|-----------|--------------|:------------:|
| **BFS** | Busca em largura, caminho mínimo (sem peso), conexidade, bipartido | O(V + E) |
| **DFS** | Busca em profundidade, ciclos, componentes conexas, ordenação topológica | O(V + E) |
| **Dijkstra** | Caminho mínimo com pesos **não negativos** | O(E + V log V) |
| **Bellman-Ford** | Caminho mínimo com pesos **negativos** (detecta ciclos negativos) | O(VE) |
| **Floyd-Warshall** | Caminho mínimo entre **todos** os pares de vértices | O(V³) |
| **Guloso** | Paradigma geral: escolha local ótima a cada passo (Kruskal, Prim, Dijkstra...) | Depende |
| **Welsh-Powell** | Coloração de vértices (heurística gulosa por grau decrescente) | O(V²) |
| **Ford-Fulkerson** | Fluxo máximo em rede | O(E × f*) |
| **Edmonds-Karp** | Fluxo máximo (Ford-Fulkerson com BFS) | O(VE²) |
| **Dinic** | Fluxo máximo (mais eficiente) | O(V²E) |
| **Kosaraju** | Componentes fortemente conexas (grafo direcionado) | O(V + E) |
| **Ordenação Topológica** | Ordenar vértices de DAG respeitando dependências | O(V + E) |
| **Kahn** | Ordenação topológica (por grau de entrada) | O(V + E) |
| **Prim** | Árvore geradora mínima (expande de um vértice) | O(E + V log V) |
| **Kruskal** | Árvore geradora mínima (ordena arestas, usa Union-Find) | O(E log E) |

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

### G1 — Maior valor de um vetor

**Problema de decisão:** "Dado vetor V de n elementos e valor k, o maior valor de V é ≥ k?"

**Certificado +:** Índice i com V[i] ≥ k e V[i] = max. Verificação: percorrer o vetor confirmando → O(n).  
**Certificado −:** Percorrer e verificar que todos < k → O(n).

**Resolução:** Percorrer o vetor uma vez → O(n) → polinomial.

**Classe: P, NP e co-NP.** Existe algoritmo polinomial, logo pertence às três.

---

### G2 — Número primo

**Problema de decisão:** "Dado inteiro n, n é primo?"

**Certificado +:** Certificado de Pratt (verificação polinomial). Ou como está em P, certificado vazio — rodar o algoritmo basta.  
**Certificado −:** Divisor d com 1 < d < n e d | n → verificação O(log² n).

**Resolução:** Teste AKS (2002) → tempo polinomial.

**Classe: P, NP e co-NP.**

---

### G3 — Ordenar vetor

**Problema de decisão:** "Dado vetor V, é possível ordená-lo em ordem crescente?" (trivialmente SIM). Versão útil: "V já está ordenado?"

**Certificado +:** O vetor ordenado → checar V[i] ≤ V[i+1] → O(n).  
**Certificado −:** Par (i, i+1) com V[i] > V[i+1] → O(1).

**Resolução:** Merge Sort → O(n log n) → polinomial.

**Classe: P, NP e co-NP.**

---

### G4 — Grafo hamiltoniano

**Problema de decisão:** "Dado grafo G, existe ciclo que passe por todos os vértices exatamente uma vez?"

**Certificado +:** Sequência de vértices do ciclo → checar que todos aparecem uma vez e arestas existem → O(V).  
**Certificado −:** Não se conhece certificado polinomial genérico para provar que NÃO existe hamiltoniano.

**Resolução:** Não se conhece algoritmo polinomial. Melhores algoritmos conhecidos são exponenciais.

**Classe: NP (com certeza). Não se sabe se está em P ou co-NP.**

---

### G5 — Grafo euleriano

**Problema de decisão:** "Dado grafo conexo G, existe circuito que percorra todas as arestas exatamente uma vez?"

**Certificado +:** Sequência de arestas do circuito → checar que cada aresta aparece uma vez e forma circuito → O(E).  
**Certificado −:** Vértice com grau ímpar → contar arestas incidentes → O(grau).

**Resolução:** Teorema de Euler → existe ⟺ conexo + todos os vértices com grau par. Verificar com **BFS/DFS** + checar graus → O(V + E) → polinomial.

**Classe: P, NP e co-NP.**

> ⚠️ Euler (arestas) → P. Hamilton (vértices) → não se sabe se P.

---

### G6 — Árvore geradora

**Problema de decisão:** "Dado grafo G, existe árvore geradora?" (= "G é conexo?")

**Certificado +:** A árvore (V-1 arestas) → verificar conexidade e aciclo → O(V + E).  
**Certificado −:** Dois vértices u, v sem caminho → BFS de u, v não alcançado → O(V + E).

**Resolução:** **BFS/DFS** para conexidade → O(V + E). **Kruskal** O(E log V) ou **Prim** O(E + V log V) para construir a árvore.

**Classe: P, NP e co-NP.**

---

### G7 — 3-coloração

**Problema de decisão:** "Dado grafo G, é possível colorir vértices com ≤ 3 cores sem adjacentes iguais?"

**Certificado +:** Atribuição de cores → checar cada aresta cor(u) ≠ cor(v) → O(E).  
**Certificado −:** Não se conhece certificado polinomial genérico (teria que testar 3^V atribuições).

**Resolução:** Não se conhece algoritmo polinomial. (**Welsh-Powell** é heurística gulosa — não garante ótimo nem decide se é 3-colorável.)

**Classe: NP (com certeza). Não se sabe se está em P ou co-NP.**

---

### G8 — 2-coloração

**Problema de decisão:** "Dado grafo G, é possível colorir com 2 cores sem adjacentes iguais?"

**Certificado +:** Atribuição de 2 cores → checar cada aresta → O(E).  
**Certificado −:** Ciclo de comprimento ímpar → percorrer e confirmar → O(V).

**Resolução:** 2-colorável ⟺ bipartido ⟺ sem ciclos ímpares. **BFS** modificada → O(V + E) → polinomial.

**Classe: P, NP e co-NP.**

> ⚠️ 2-coloração → P. 3-coloração → não se sabe se P.

---

### G9 — Maior clique

**Problema de decisão:** "Dado grafo G e inteiro k, existe clique de tamanho ≥ k?"

**Certificado +:** Conjunto de k vértices → checar todos os pares adjacentes → O(k²).  
**Certificado −:** Não se conhece certificado polinomial genérico.

**Resolução:** Não se conhece algoritmo polinomial.

**Classe: NP (com certeza). Não se sabe se está em P ou co-NP.**

---

### G10 — Conjunto independente máximo

**Problema de decisão:** "Dado grafo G e inteiro k, existe conjunto independente de tamanho ≥ k?"

**Certificado +:** Conjunto de k vértices → checar que nenhum par é adjacente → O(k²).  
**Certificado −:** Não se conhece certificado polinomial genérico.

**Resolução:** Não se conhece algoritmo polinomial. (Relação: independente em G = clique no complemento Ḡ.)

**Classe: NP (com certeza). Não se sabe se está em P ou co-NP.**

---

### G11 — Cobertura mínima de vértices

**Problema de decisão:** "Dado grafo G e inteiro k, existe cobertura de vértices de tamanho ≤ k?"

**Certificado +:** Conjunto de ≤ k vértices → para cada aresta (u,v), checar u ∈ C ou v ∈ C → O(E).  
**Certificado −:** Não se conhece certificado polinomial genérico.

**Resolução:** Não se conhece algoritmo polinomial. (Relação: C é cobertura ⟺ V \ C é independente.)

**Classe: NP (com certeza). Não se sabe se está em P ou co-NP.**

---

### G12 — Cobertura mínima de arestas

**Problema de decisão:** "Dado grafo G sem vértices isolados e inteiro k, existe cobertura de arestas de tamanho ≤ k?"

**Certificado +:** Conjunto de ≤ k arestas → checar todo vértice incidente a alguma aresta → O(V + k).  
**Certificado −:** Como está em P, rodar o algoritmo basta.

**Resolução:** Emparelhamento máximo + extensão gulosa. Pode usar **Edmonds-Karp** (fluxo máximo em rede bipartida) ou **Ford-Fulkerson** para o emparelhamento → polinomial.

**Classe: P, NP e co-NP.**

> ⚠️ Cobertura de **vértices** → não se sabe se P. Cobertura de **arestas** → P.

---

### G13 — Contar subconjuntos

**Problema de decisão:** "Dado conjunto S de n elementos, quantidade de subconjuntos ≥ k?"

**Certificado +:** Valor 2^n → calcular e confirmar ≥ k → O(n).  
**Certificado −:** Valor 2^n → calcular e confirmar < k → O(n).

**Resolução:** Sempre 2^n subconjuntos. Calcular 2^n → O(n) multiplicações. Comparar com k → O(1). Polinomial.

**Classe: P, NP e co-NP.**

**Atenção:** *Contar* → P. *Listar* todos os 2^n → exponencial (output exponencial).

---

## Tabela Resumo

| # | Problema | P? | NP? | co-NP? | Algoritmo que resolve |
|---|----------|----|-----|--------|----------------------|
| 1 | Maior valor do vetor | ✅ | ✅ | ✅ | Percorrer vetor O(n) |
| 2 | Número primo | ✅ | ✅ | ✅ | AKS |
| 3 | Ordenar vetor | ✅ | ✅ | ✅ | Merge Sort |
| 4 | Grafo hamiltoniano | ❓ | ✅ | ❓ | Sem algoritmo polinomial |
| 5 | Grafo euleriano | ✅ | ✅ | ✅ | BFS/DFS + checar graus |
| 6 | Árvore geradora | ✅ | ✅ | ✅ | Kruskal / Prim / BFS |
| 7 | 3-coloração | ❓ | ✅ | ❓ | Sem algoritmo polinomial |
| 8 | 2-coloração | ✅ | ✅ | ✅ | BFS (bipartido) |
| 9 | Maior clique | ❓ | ✅ | ❓ | Sem algoritmo polinomial |
| 10 | Conj. independ. máx. | ❓ | ✅ | ❓ | Sem algoritmo polinomial |
| 11 | Cobert. mín. vértices | ❓ | ✅ | ❓ | Sem algoritmo polinomial |
| 12 | Cobert. mín. arestas | ✅ | ✅ | ✅ | Edmonds-Karp / Ford-Fulkerson |
| 13 | Contar subconjuntos | ✅ | ✅ | ✅ | Calcular 2^n |

**Legenda:** ✅ = sim · ❓ = não se sabe

---

## Tabela para Decorar — Algoritmo → Problema

| Algoritmo | Serve para | Tipo |
|-----------|-----------|------|
| **BFS** | Conexidade, bipartido (2-cor), caminho mín. sem peso, Euler | Busca |
| **DFS** | Conexidade, ciclos, componentes, ord. topológica, Euler | Busca |
| **Dijkstra** | Caminho mínimo (pesos ≥ 0) | Caminho |
| **Bellman-Ford** | Caminho mínimo (pesos negativos OK) | Caminho |
| **Floyd-Warshall** | Caminho mín. todos-pra-todos | Caminho |
| **Prim** | Árvore geradora mínima | AGM |
| **Kruskal** | Árvore geradora mínima | AGM |
| **Ford-Fulkerson** | Fluxo máximo → emparelhamento → cobert. arestas | Fluxo |
| **Edmonds-Karp** | Fluxo máximo (Ford-Fulkerson + BFS) | Fluxo |
| **Dinic** | Fluxo máximo (mais rápido) | Fluxo |
| **Welsh-Powell** | Coloração gulosa (heurística, não garante ótimo) | Coloração |
| **Kosaraju** | Componentes fortemente conexas | Grafos dir. |
| **Ord. Topológica** | Ordenar DAG por dependências | Grafos dir. |
| **Kahn** | Ord. topológica por grau de entrada | Grafos dir. |

### Macetes para decorar

- **Caminho mínimo sem peso?** → BFS
- **Caminho mínimo com peso ≥ 0?** → Dijkstra
- **Caminho mínimo com peso negativo?** → Bellman-Ford
- **Caminho mínimo todos-todos?** → Floyd-Warshall
- **Árvore geradora?** → Prim ou Kruskal
- **Fluxo / emparelhamento / cobertura de arestas?** → Ford-Fulkerson / Edmonds-Karp
- **Bipartido / 2-coloração?** → BFS
- **Euleriano?** → BFS/DFS + graus pares
- **Componentes fortemente conexas?** → Kosaraju ou DFS duas vezes
- **Ordenar DAG?** → Kahn ou DFS com pilha
