# 20 Exercícios Extras — P, NP e co-NP (CLRS 34.1 e 34.2)

**Disciplina:** Fundamentos de Projeto e Análise de Algoritmos · PUC Minas  

Para cada exercício: identifique o problema de decisão, forneça certificado positivo e negativo, classifique em P, NP e/ou co-NP e justifique.

---

## FÁCIL

### Ex. 1
Buscar um elemento em um vetor.

### Ex. 2
Verificar se um grafo é conexo.

### Ex. 3
Verificar se um vetor já está em ordem crescente.

### Ex. 4
Encontrar o MDC de dois números inteiros.

### Ex. 5
Verificar se um grafo contém algum ciclo.

### Ex. 6
Verificar se o produto de duas matrizes A e B é igual a uma dada matriz C.

### Ex. 7
Encontrar o caminho de menor peso entre dois vértices de um grafo.

---

## MÉDIO

### Ex. 8
Dado um conjunto S de inteiros e um valor t, determinar se existe subconjunto de S cuja soma é exatamente t (Subset Sum).

### Ex. 9
Encontrar o caminho simples mais longo entre dois vértices de um grafo.

### Ex. 10
Dada uma fórmula booleana em forma normal conjuntiva (CNF), determinar se ela é satisfatível (SAT).

### Ex. 11
Dada uma fórmula booleana em CNF com exatamente 2 literais por cláusula, determinar se ela é satisfatível (2-SAT).

### Ex. 12
Dados n itens com pesos e valores, uma capacidade W e um valor alvo V, determinar se existe subconjunto de itens que cabe na mochila e tem valor total ≥ V (Problema da Mochila).

### Ex. 13
Dado um grafo, determinar se existe emparelhamento (matching) perfeito.

### Ex. 14
Dados dois grafos G₁ e G₂, determinar se são isomorfos.

---

## DIFÍCIL

### Ex. 15
Dado um grafo completo ponderado e um inteiro k, determinar se existe ciclo hamiltoniano com peso total ≤ k (TSP — Caixeiro Viajante).

### Ex. 16
Dado um inteiro n e um inteiro k, determinar se n possui algum fator primo ≤ k (Fatoração).

### Ex. 17
Dado um conjunto S de inteiros, determinar se é possível particioná-lo em dois subconjuntos com a mesma soma (Partição).

### Ex. 18
Dado um inteiro n, determinar se n é composto (não primo).

### Ex. 19
Dado um grafo G e um inteiro k (com k ≥ 3), determinar se G é k-colorável.

### Ex. 20
Dado um sistema de inequações lineares Ax ≤ b, determinar se existe vetor x que satisfaça todas as restrições (Programação Linear).

---
---
---

# GABARITO

---

## Gabarito — Fácil

---

### G1 — Busca em vetor

**Decisão:** "Dado vetor V e valor x, existe V[i] = x?"  
**Certificado +:** Índice i com V[i] = x → verificação O(1).  
**Certificado −:** Percorrer tudo e confirmar que x não aparece → O(n).  
**Resolução:** Busca linear O(n) → polinomial.  
**Classe: P, NP e co-NP.**

---

### G2 — Grafo conexo

**Decisão:** "Dado grafo G, G é conexo?"  
**Certificado +:** Árvore geradora → verificação O(V + E).  
**Certificado −:** Dois vértices u, v sem caminho entre eles → BFS de u, v não alcançado → O(V + E).  
**Resolução:** BFS/DFS → O(V + E).  
**Classe: P, NP e co-NP.**

---

### G3 — Vetor ordenado

**Decisão:** "Dado vetor V, V está em ordem crescente?"  
**Certificado +:** Certificado vazio — rodar o algoritmo → O(n).  
**Certificado −:** Par (i, i+1) com V[i] > V[i+1] → O(1).  
**Resolução:** Percorrer checando V[i] ≤ V[i+1] → O(n).  
**Classe: P, NP e co-NP.**

---

### G4 — MDC

**Decisão:** "Dados a, b e k, MDC(a,b) ≥ k?"  
**Certificado +:** Valor d = MDC(a,b) com d ≥ k → checar d | a, d | b → O(log n).  
**Certificado −:** Valor d = MDC(a,b) com d < k → mesma verificação.  
**Resolução:** Algoritmo de Euclides → O(log(min(a,b))).  
**Classe: P, NP e co-NP.**

---

### G5 — Ciclo em grafo

**Decisão:** "Dado grafo G, G contém algum ciclo?"  
**Certificado +:** Sequência de vértices do ciclo → O(k), k = tamanho do ciclo.  
**Certificado −:** Floresta geradora (se é floresta, não tem ciclo) → O(V + E).  
**Resolução:** DFS detecta ciclo em O(V + E).  
**Classe: P, NP e co-NP.**

---

### G6 — Multiplicação de matrizes

**Decisão:** "Dadas A, B, C, temos A×B = C?"  
**Certificado +:** A própria C → calcular A×B e comparar → O(n³).  
**Certificado −:** Posição (i,j) com (A×B)[i][j] ≠ C[i][j] → calcular uma posição → O(m).  
**Resolução:** Multiplicação O(n³), Strassen O(n^2.81), verificação de Freivalds O(n²).  
**Classe: P, NP e co-NP.**

---

### G7 — Caminho mais curto

**Decisão:** "Dado grafo G com pesos, vértices s e t, e valor k, existe caminho de s a t com peso ≤ k?"  
**Certificado +:** O caminho → somar pesos, checar ≤ k → O(V).  
**Certificado −:** Como está em P, rodar o algoritmo basta.  
**Resolução:** Dijkstra O(E + V log V) ou Bellman-Ford O(VE).  
**Classe: P, NP e co-NP.**

---

## Gabarito — Médio

---

### G8 — Subset Sum

**Decisão:** "Dado conjunto S e alvo t, existe subconjunto com soma = t?"  
**Certificado +:** O subconjunto → somar e checar = t → O(n).  
**Certificado −:** Não se conhece certificado polinomial genérico.  
**Resolução:** NP-Completo (Karp, 1972). Sem algoritmo polinomial conhecido.  
**Classe: NP e NP-Completo. Não se sabe se P ou co-NP.**

---

### G9 — Caminho simples mais longo

**Decisão:** "Dado grafo G, vértices s, t e inteiro k, existe caminho simples de s a t com ≥ k arestas?"  
**Certificado +:** O caminho → checar simplicidade + contar arestas → O(V).  
**Certificado −:** Não se conhece certificado polinomial genérico.  
**Resolução:** NP-Completo. Contraste direto: caminho mais **curto** → P, mais **longo** → NP-C.  
**Classe: NP e NP-Completo. Não se sabe se P ou co-NP.**

---

### G10 — SAT

**Decisão:** "Dada fórmula φ em CNF, existe atribuição que a torne verdadeira?"  
**Certificado +:** Atribuição (x₁ = V, x₂ = F, ...) → avaliar φ → O(|φ|).  
**Certificado −:** Não se conhece certificado polinomial genérico.  
**Resolução:** NP-Completo (Cook-Levin, 1971 — primeiro NP-C provado).  
**Classe: NP e NP-Completo. Não se sabe se P ou co-NP.**

---

### G11 — 2-SAT

**Decisão:** "Dada fórmula em CNF com exatamente 2 literais por cláusula, é satisfatível?"  
**Certificado +:** Atribuição satisfatória → avaliar fórmula → O(m).  
**Certificado −:** Como está em P, rodar o algoritmo basta.  
**Resolução:** Componentes fortemente conexas (Tarjan) → O(n + m). Polinomial.  
**Classe: P, NP e co-NP.**

> ⚠️ 2-SAT → P. 3-SAT → NP-Completo.

---

### G12 — Problema da Mochila

**Decisão:** "Dados itens com pesos wᵢ e valores vᵢ, capacidade W e alvo V, existe subconjunto com peso ≤ W e valor ≥ V?"  
**Certificado +:** O subconjunto → somar pesos e valores → O(n).  
**Certificado −:** Não se conhece certificado polinomial genérico.  
**Resolução:** NP-Completo (geral). PD O(nW) é pseudopolinomial (polinomial no valor de W, exponencial no tamanho log W).  
**Classe: NP e NP-Completo. Não se sabe se P ou co-NP.**

---

### G13 — Emparelhamento perfeito

**Decisão:** "Dado grafo G, existe emparelhamento que cobre todos os vértices?"  
**Certificado +:** O emparelhamento → checar cobertura total → O(V + E).  
**Certificado −:** Pelo Teorema de Tutte: conjunto S com G - S tendo mais componentes ímpares que |S| → verificação polinomial.  
**Resolução:** Edmonds (Blossom) → O(V³).  
**Classe: P, NP e co-NP.**

---

### G14 — Isomorfismo de grafos

**Decisão:** "Dados G₁ e G₂, são isomorfos?"  
**Certificado +:** Bijeção f: V₁ → V₂ preservando adjacências → O(V + E).  
**Certificado −:** Não se conhece certificado polinomial simples (existe protocolo interativo).  
**Resolução:** Não se sabe se P. Acredita-se que NÃO é NP-C. Babai (2015) → quase-polinomial.  
**Classe: NP (e provavelmente co-NP). "No limbo" — não se sabe se P nem se NP-C.**

---

## Gabarito — Difícil

---

### G15 — TSP (Caixeiro Viajante)

**Decisão:** "Dado grafo completo ponderado e inteiro k, existe ciclo hamiltoniano com peso ≤ k?"  
**Certificado +:** O ciclo → somar pesos + checar que visita todos → O(V).  
**Certificado −:** Não se conhece certificado polinomial genérico.  
**Resolução:** NP-Completo. TSP é "mais difícil" que Hamilton (Hamilton é caso especial com pesos 1 e k = V).  
**Classe: NP e NP-Completo. Não se sabe se P ou co-NP.**

---

### G16 — Fatoração de inteiros

**Decisão:** "Dado inteiro n e inteiro k, n tem fator primo ≤ k?"  
**Certificado +:** Fator primo p ≤ k → checar p | n e p primo → polinomial.  
**Certificado −:** Fatoração completa com todos os fatores > k → multiplicar e checar = n → polinomial.  
**Resolução:** Não se sabe se P. Acredita-se que NÃO é NP-C (se fosse, RSA quebraria). Outro problema "no limbo".  
**Classe: NP ∩ co-NP (ambos certificados existem). Não se sabe se P. Provavelmente não NP-C.**

---

### G17 — Partição

**Decisão:** "Dado conjunto S de inteiros, é possível dividir em dois subconjuntos com mesma soma?"  
**Certificado +:** Os dois subconjuntos → somar cada um e comparar → O(n).  
**Certificado −:** Não se conhece certificado polinomial genérico. (Se soma total ímpar → trivialmente NÃO.)  
**Resolução:** NP-Completo (caso especial do Subset Sum).  
**Classe: NP e NP-Completo. Não se sabe se P ou co-NP.**

---

### G18 — Número composto

**Decisão:** "Dado inteiro n, n é composto (não primo)?"  
**Certificado +:** Divisor d com 1 < d < n → checar d | n → O(log² n).  
**Certificado −:** Certificado de primalidade (Pratt) → polinomial.  
**Resolução:** Complemento de primo. Como primo ∈ P (AKS) → composto ∈ P.  
**Classe: P, NP e co-NP.**

**Perceba:** COMPOSTO ∈ NP (certificado = divisor) → PRIMO ∈ co-NP. Como ambos estão em P, estão nas três classes.

---

### G19 — k-Coloração (k ≥ 3)

**Decisão:** "Dado grafo G e inteiro k ≥ 3, é possível colorir G com k cores sem adjacentes iguais?"  
**Certificado +:** Atribuição de cores → checar cada aresta → O(E).  
**Certificado −:** Não se conhece certificado polinomial genérico para k ≥ 3.  
**Resolução:** NP-Completo para k ≥ 3. Para k = 1 (trivial, grafo sem arestas) e k = 2 (bipartido) → P.  
**Classe: NP e NP-Completo (k ≥ 3). Não se sabe se P ou co-NP.**

---

### G20 — Programação Linear

**Decisão:** "Dado sistema Ax ≤ b, existe vetor x viável?"  
**Certificado +:** Vetor x → calcular Ax e checar ≤ b → O(mn).  
**Certificado −:** Pelo Lema de Farkas: vetor dual y ≥ 0 com yᵀA = 0 e yᵀb < 0 → verificação polinomial.  
**Resolução:** Método do elipsoide (Khachiyan, 1979), pontos interiores (Karmarkar, 1984) → polinomial.  
**Classe: P, NP e co-NP.**

**Contraste:** Programação **Linear** → P. Programação **Inteira** → NP-Completo.

---

## Tabela Resumo

| # | Problema | P? | NP? | co-NP? | NP-C? | Nível |
|---|----------|----|-----|--------|-------|-------|
| 1 | Busca em vetor | ✅ | ✅ | ✅ | ❌ | Fácil |
| 2 | Grafo conexo | ✅ | ✅ | ✅ | ❌ | Fácil |
| 3 | Vetor ordenado | ✅ | ✅ | ✅ | ❌ | Fácil |
| 4 | MDC | ✅ | ✅ | ✅ | ❌ | Fácil |
| 5 | Ciclo em grafo | ✅ | ✅ | ✅ | ❌ | Fácil |
| 6 | Mult. matrizes | ✅ | ✅ | ✅ | ❌ | Fácil |
| 7 | Caminho mais curto | ✅ | ✅ | ✅ | ❌ | Fácil |
| 8 | Subset Sum | ❓ | ✅ | ❓ | ✅ | Médio |
| 9 | Caminho mais longo | ❓ | ✅ | ❓ | ✅ | Médio |
| 10 | SAT | ❓ | ✅ | ❓ | ✅ | Médio |
| 11 | 2-SAT | ✅ | ✅ | ✅ | ❌ | Médio |
| 12 | Mochila | ❓ | ✅ | ❓ | ✅ | Médio |
| 13 | Emparelham. perfeito | ✅ | ✅ | ✅ | ❌ | Médio |
| 14 | Isomorf. grafos | ❓ | ✅ | ✅* | ❓ | Médio |
| 15 | TSP | ❓ | ✅ | ❓ | ✅ | Difícil |
| 16 | Fatoração | ❓ | ✅ | ✅ | ❓ | Difícil |
| 17 | Partição | ❓ | ✅ | ❓ | ✅ | Difícil |
| 18 | Nº composto | ✅ | ✅ | ✅ | ❌ | Difícil |
| 19 | k-Coloração (k≥3) | ❓ | ✅ | ❓ | ✅ | Difícil |
| 20 | Prog. Linear | ✅ | ✅ | ✅ | ❌ | Difícil |

**Legenda:** ✅ = sim · ❓ = não se sabe · ❌ = não
