# Simulado de Prova — Classe P, NP e co-NP (CLRS 34.1 e 34.2)

**Pontifícia Universidade Católica de Minas Gerais**  
Instituto de Ciências Exatas e Informática  
Prova 2 — 1/2026  
Prof. Felipe Belém (felipebelem@pucminas.br)  

**NOME:** _________________________________________________ **NOTA:** ___ em 25  

**Obs.:** (i) a atividade é INDIVIDUAL; (ii) respostas devem ser legíveis, à caneta, claras e objetivas; (iii) respostas SEM justificativa ou demonstração serão DESCONSIDERADAS.

---

## Q1. [6 pts — 1 pt cada] Verifique se as afirmações são verdadeiras ou falsas. Explique BREVEMENTE.

**a)** Todo problema em P também está em NP.

**b)** Se um problema é NP-Completo e alguém encontrar um algoritmo polinomial para ele, então P = NP.

**c)** O problema da 2-coloração de grafos é NP-Completo.

**d)** NP significa "Não Polinomial".

**e)** Um problema que está em P não pode estar em co-NP.

**f)** Se um problema está em NP, então necessariamente ele não está em P.

---

## Q2. [6 pts — 3 pts cada] Classifique em P, NP e/ou co-NP. Forneça o problema de decisão, certificado positivo e negativo. Justifique.

**a)** Verificar se um grafo possui circuito euleriano.

**b)** Dado um grafo G e um inteiro k, determinar se G possui uma clique de tamanho ≥ k.

---

## Q3. [4 pts] Prove que P ⊆ NP. Ou seja, mostre que se uma linguagem L pertence a P, então L pertence a NP.

---

## Q4. [4 pts] Explique, com um exemplo concreto, a diferença entre um algoritmo que **aceita** uma linguagem e um que **decide** uma linguagem. Por que essa distinção é importante para a definição da Classe P?

---

## Q5. [5 pts] Considere os seguintes problemas. Para cada par, explique por que um está em P e o outro é NP-Completo, apesar de parecerem semelhantes.

**a)** Circuito de Euler vs. Circuito Hamiltoniano.

**b)** 2-SAT vs. 3-SAT.

---
---
---

# GABARITO

---

### Gabarito Q1

**a) VERDADEIRO.** Se L ∈ P, existe algoritmo polinomial A que decide L. Para verificar, use certificado vazio: o verificador roda A(x) e ignora o certificado. Como A é polinomial, a verificação é polinomial → L ∈ NP. Logo P ⊆ NP.

**b) VERDADEIRO.** Por definição de NP-Completo, todo problema em NP pode ser reduzido em tempo polinomial a qualquer NP-C. Se esse NP-C tem algoritmo polinomial, a composição (redução + solução, ambas polinomiais) resolve qualquer problema NP em tempo polinomial → P = NP.

**c) FALSO.** 2-coloração equivale a verificar se o grafo é bipartido → BFS em O(V + E) → está em P. Problemas em P não são NP-Completos (assumindo P ≠ NP, que é a conjectura amplamente aceita).

**d) FALSO.** NP significa *Nondeterministic Polynomial* — polinomial em uma máquina de Turing não-determinística. NÃO significa "Não Polinomial". Aliás, todo problema em P também está em NP.

**e) FALSO.** Na verdade, P ⊆ co-NP. Se L ∈ P, então o complemento L̄ também está em P (basta inverter a saída). Como L̄ ∈ P ⊆ NP, temos L ∈ co-NP por definição.

**f) FALSO.** P ⊆ NP, portanto todo problema em P está em NP. Estar em NP não significa que o problema é difícil — significa apenas que o SIM pode ser verificado em tempo polinomial. Problemas em P satisfazem isso trivialmente.

---

### Gabarito Q2

**a) Circuito Euleriano**

*Problema de decisão:* "Dado grafo conexo G, existe circuito que percorra todas as arestas exatamente uma vez?"

*Certificado +:* Sequência de arestas do circuito → checar que toda aresta aparece uma vez e forma circuito → O(E).

*Certificado −:* Um vértice com grau ímpar → contar arestas incidentes → O(grau do vértice).

*Classe:* **P, NP e co-NP.** Pelo Teorema de Euler: existe circuito euleriano ⟺ grafo conexo + todos os vértices com grau par. Verificável em O(V + E).

**b) Clique de tamanho k**

*Problema de decisão:* "Dado grafo G e inteiro k, existe clique (subgrafo completo) de tamanho ≥ k?"

*Certificado +:* Conjunto de k vértices → checar que todos os pares são adjacentes → O(k²) ⊆ O(V²). Verificação polinomial.

*Certificado −:* Não se conhece certificado polinomial genérico para provar que não existe clique de tamanho k.

*Classe:* **NP e NP-Completo** (um dos 21 problemas de Karp, 1972). Não se sabe se está em P ou co-NP.

---

### Gabarito Q3

**Prova de P ⊆ NP:**

Seja L ∈ P. Então existe algoritmo determinístico A que decide L em tempo polinomial O(n^k) para alguma constante k.

Precisamos mostrar que L ∈ NP, ou seja, que existe um verificador de tempo polinomial para L.

Construímos o verificador V(x, y) da seguinte forma:
- V ignora o certificado y.
- V simplesmente executa A(x).
- Se A(x) = 1 (aceita), V retorna 1.
- Se A(x) = 0 (rejeita), V retorna 0.

**Corretude:**
- Se x ∈ L: A(x) = 1, portanto V(x, ε) = 1. Existe certificado (y = ε, o certificado vazio) tal que V aceita.
- Se x ∉ L: A(x) = 0, portanto V(x, y) = 0 para todo y. Nenhum certificado faz V aceitar.

**Tempo:** V roda em tempo O(n^k), que é polinomial.

Logo L ∈ NP, e como L foi arbitrário, P ⊆ NP. ∎

---

### Gabarito Q4

**Aceitar vs. Decidir:**

- **Aceitar:** O algoritmo retorna 1 para strings em L, mas pode **rodar para sempre** (não parar) para strings fora de L. Ele só garante a resposta quando é SIM.

- **Decidir:** O algoritmo retorna 1 para strings em L e retorna 0 para strings fora de L. Ele **sempre para** e dá a resposta correta em ambos os casos.

**Exemplo concreto:** Considere a linguagem L = {x ∈ {0,1}* : x codifica um grafo conexo}.

- *Algoritmo que aceita L:* Enumera todos os possíveis caminhos entre todos os pares de vértices. Se encontrar caminhos para todos os pares, retorna 1. Se o grafo não for conexo, ele pode ficar tentando encontrar caminhos para sempre (dependendo da implementação).

- *Algoritmo que decide L:* Roda BFS a partir de qualquer vértice. Se todos os vértices forem visitados, retorna 1. Senão retorna 0. **Sempre para** em O(V + E).

**Importância para P:** A definição de P exige algoritmos que **decidem** (sempre param em tempo polinomial). Se permitíssemos apenas "aceitar", um algoritmo poderia rodar eternamente para instâncias NÃO, e não teríamos garantia de tempo polinomial para todas as entradas.

---

### Gabarito Q5

**a) Euler vs. Hamilton**

- **Circuito de Euler** (percorrer todas as **arestas** uma vez): está em **P** porque, pelo Teorema de Euler, basta verificar se o grafo é conexo e todos os vértices têm grau par → O(V + E). A condição é simples e verificável localmente (grau de cada vértice).

- **Circuito Hamiltoniano** (percorrer todos os **vértices** uma vez): é **NP-Completo** porque não existe condição local simples como "grau par" para garantir existência. A única forma conhecida de resolver na generalidade é testar combinações de caminhos, o que é exponencial. A diferença é que a estrutura de arestas (Euler) permite uma caracterização elegante, enquanto a estrutura de vértices (Hamilton) não.

**b) 2-SAT vs. 3-SAT**

- **2-SAT** (cláusulas com 2 literais): está em **P** porque cada cláusula (a ∨ b) equivale a duas implicações (¬a → b e ¬b → a). Isso forma um grafo de implicações, e a fórmula é satisfatível se e somente se nenhuma variável x e sua negação ¬x estão na mesma componente fortemente conexa. Algoritmo de Tarjan → O(n + m).

- **3-SAT** (cláusulas com 3 literais): é **NP-Completo** (Cook-Levin + redução). Com 3 literais por cláusula, a técnica do grafo de implicações não funciona — uma cláusula (a ∨ b ∨ c) gera implicações condicionais que criam dependências complexas demais. O número de combinações possíveis explode e não se conhece atalho polinomial.

**A lição:** Um único literal a mais por cláusula destrói a estrutura que permite a solução eficiente.

---

## Dicas finais para a prova do Felipe

1. **Sempre justifique.** Sem justificativa = zero.
2. **Seja claro e objetivo.** V/F: 2-3 linhas bastam.
3. **Roteiro para classificar:** (1) problema de decisão, (2) tentar algoritmo polinomial, (3) certificado +, (4) certificado −, (5) conclusão.
4. **Certificados:** diga o que é, como verificar, e o custo.
5. **Decore os contrastes:** Euler/Hamilton, 2-SAT/3-SAT, 2-cor/3-cor, curto/longo, vértices/arestas.
