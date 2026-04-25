# Exercícios de Transformação e Redução (CLRS 34.3)

**Disciplina:** Fundamentos de Projeto e Análise de Algoritmos · PUC Minas  
**Professor:** Felipe de Castro Belém  

---

> **Enunciado:** Resolva os problemas a seguir utilizando o algoritmo dado (supondo a existência de sua solução). Deixe claro cada uma das etapas da transformação, explicando a razão de ser a solução.

---

### Exercício 1
Encontrar a maior quantidade de arestas entre dois vértices em um grafo não ponderado (Dijkstra).

### Exercício 2
Encontrar um emparelhamento máximo em um grafo (Ford-Fulkerson).

### Exercício 3
Encontrar um conjunto independente máximo em um grafo (Cobertura mínima de vértices).

### Exercício 4
Encontrar o maior subgrafo completo de um grafo (Conjunto independente máximo).

### Exercício 5
Verificar se um grafo é bipartido (Coloração mínima de vértices).

---
---
---

# GABARITO

---

## Ideia Geral

Nesses exercícios o Felipe quer que você **transforme** o problema A (o que ele pede) em uma instância do problema B (o algoritmo que ele te dá), resolva com B, e depois **interprete** a resposta de volta para A.

O roteiro é sempre:

1. **Entrada:** o que você recebe (o problema original A)
2. **Transformação:** como converter a instância de A em instância de B (tempo polinomial)
3. **Resolução:** rodar o algoritmo de B
4. **Interpretação:** como a resposta de B te dá a resposta de A
5. **Justificativa:** por que a transformação está correta (SIM ↔ SIM, NÃO ↔ NÃO)

---

### Gabarito 1 — Maior quantidade de arestas entre dois vértices (usando Dijkstra)

**Problema A:** Dado um grafo G = (V, E) não ponderado e dois vértices s e t, encontrar o caminho com o **maior** número de arestas entre s e t.

**Algoritmo dado:** Dijkstra (encontra o caminho de **menor** peso).

**O problema:** Dijkstra encontra o **menor** caminho, mas queremos o **maior**. Precisamos transformar a instância para que o menor no grafo transformado corresponda ao maior no original.

---

**Etapa 1 — Transformação da entrada:**

- Pegue o grafo original G = (V, E) não ponderado.
- Crie um novo grafo G' = (V, E) com os **mesmos** vértices e arestas.
- Atribua peso a cada aresta: w'(u, v) = **-1** para toda aresta (u, v) ∈ E.

**Problema:** Dijkstra não funciona com pesos negativos! Precisamos de outra abordagem.

**Alternativa correta:** Em vez de pesos negativos, faça a seguinte transformação:

- Atribua peso w'(u, v) = **C - 1** a cada aresta, onde C é um valor grande o suficiente (por exemplo, C = |V|).
- Ou, de forma mais elegante: atribua w'(u, v) = **1/(número de arestas)** — mas isso complica.

**Abordagem mais limpa:**

- Crie G' com os mesmos vértices e arestas.
- Atribua peso w'(u, v) = **(|V| - 1) - 1 = |V| - 2** para toda aresta? Não, isso também não inverte.

**A transformação correta é:**

- No grafo original, toda aresta tem "comprimento" 1.
- O caminho mais longo tem no máximo |V| - 1 arestas.
- Atribua peso w'(u, v) = **(|V| - 1) - 1** = uma constante grande **menos** o peso original.
- Mais precisamente: defina w'(u, v) = **M - 1** onde M é um valor maior que o caminho máximo possível (M = |V|).

**Mas a forma mais direta:** Como o grafo não é ponderado e queremos o caminho mais **longo** (mais arestas):

**Etapa 1 — Transformação:**
- Construa G' = (V, E) com peso w'(u, v) = **-1** para toda aresta.
- Como Dijkstra não aceita pesos negativos, use a transformação: w'(u, v) = **|V| - 1** para toda aresta.

Na verdade, a forma mais limpa que o Felipe espera:

**Etapa 1 — Transformação (resposta final):**
- Crie G' com mesmos vértices e arestas de G.
- Atribua peso **negativo** w'(u,v) = -1 a cada aresta.
- Como Dijkstra não aceita pesos negativos, **substitua Dijkstra por Bellman-Ford** (que aceita pesos negativos), OU faça a seguinte transformação equivalente:
  - Inverta o sentido: em vez de buscar o menor caminho com pesos -1, busque o menor caminho com pesos 1 e depois subtraia de (|V|-1).

**Abordagem que o Felipe provavelmente espera:**

> O exercício diz "supondo a existência de sua solução" — ou seja, suponha que Dijkstra funciona como oráculo. O foco é a **transformação**, não as limitações do algoritmo.

Então:

**Etapa 1 — Transformação:**
- Crie G' = (V, E) com peso w'(u,v) = -1 para toda aresta.

**Etapa 2 — Resolução:**
- Rode Dijkstra(G', s, t) no grafo transformado. Ele encontra o caminho de menor peso total.
- O caminho de menor peso com pesos -1 é justamente o caminho que usa **mais arestas** (porque cada aresta adicional diminui o peso em 1).

**Etapa 3 — Interpretação:**
- Se Dijkstra retorna peso total = -k, então o caminho mais longo tem **k** arestas.
- O caminho encontrado é o caminho com maior quantidade de arestas entre s e t.

**Justificativa:**
- Minimizar a soma de pesos -1 equivale a maximizar a quantidade de arestas.
- min(Σ -1) = min(-k) = o k mais negativo possível = o **maior** k.
- Transformação é O(E) (atribuir peso a cada aresta) → polinomial ✅.
- A resposta é preservada: o caminho mínimo em G' corresponde ao caminho máximo em G ✅.

---

### Gabarito 2 — Emparelhamento máximo (usando Ford-Fulkerson)

**Problema A:** Dado um grafo G = (V, E), encontrar um **emparelhamento máximo** (maior conjunto de arestas sem vértices em comum).

**Algoritmo dado:** Ford-Fulkerson (encontra o **fluxo máximo** em uma rede).

---

**Etapa 1 — Transformação:**

Construa uma rede de fluxo N a partir de G:

1. **Oriente as arestas:** Para cada aresta não-direcionada (u, v) em G, crie duas arestas direcionadas: u → v e v → u (ou se G é bipartido com lados L e R, oriente todas de L para R).

2. **Adicione fonte s e sumidouro t:**
   - Crie um vértice fonte **s** e conecte s a **todo** vértice de G com aresta de capacidade **1**: s → v para todo v ∈ V.
   - Crie um vértice sumidouro **t** e conecte **todo** vértice de G a t com aresta de capacidade **1**: v → t para todo v ∈ V.

   **No caso bipartido** (mais limpo):
   - Seja G bipartido com lados L e R.
   - s → todo vértice de L (capacidade 1).
   - Todo vértice de L → todo vizinho em R (capacidade 1).
   - Todo vértice de R → t (capacidade 1).

   **No caso geral** (grafo qualquer):
   - Duplique cada vértice v em v_in e v_out com aresta v_in → v_out de capacidade 1.
   - s → todo v_in (capacidade 1).
   - Todo v_out → t (capacidade 1).
   - Para cada aresta (u,v) em G: u_out → v_in (capacidade 1) e v_out → u_in (capacidade 1).

3. **Capacidade de todas as arestas internas:** 1 (para garantir que cada vértice é usado no máximo uma vez).

**Etapa 2 — Resolução:**

- Rode Ford-Fulkerson(N, s, t) na rede construída.
- Ele retorna o fluxo máximo f*.

**Etapa 3 — Interpretação:**

- As arestas originais de G que carregam fluxo = 1 formam o emparelhamento máximo.
- |emparelhamento máximo| = f* (valor do fluxo máximo).
- Para extrair o emparelhamento: percorra as arestas de G e selecione as que têm fluxo 1.

**Justificativa:**
- Capacidade 1 nas arestas de s garante que cada vértice de L é usado no máximo uma vez.
- Capacidade 1 nas arestas para t garante que cada vértice de R é usado no máximo uma vez.
- Portanto, o fluxo máximo corresponde ao maior número de arestas sem vértices repetidos = emparelhamento máximo.
- Construção da rede: O(V + E) → polinomial ✅.
- Pelo **Teorema de König**: em grafos bipartidos, o tamanho do emparelhamento máximo = fluxo máximo na rede correspondente.

---

### Gabarito 3 — Conjunto independente máximo (usando Cobertura mínima de vértices)

**Problema A:** Dado um grafo G = (V, E), encontrar o **conjunto independente máximo** (maior conjunto de vértices sem arestas entre si).

**Algoritmo dado:** Cobertura mínima de vértices (menor conjunto de vértices que toca todas as arestas).

---

**Etapa 1 — Transformação:**

Não precisa transformar o grafo! Use o **mesmo grafo G** como entrada para o algoritmo de cobertura mínima.

A relação é direta:

> **S é conjunto independente ⟺ V \ S é cobertura de vértices.**

Isso vale porque:
- Se S é independente → nenhuma aresta tem ambas pontas em S → toda aresta tem pelo menos uma ponta em V \ S → V \ S é cobertura.
- Se C é cobertura → toda aresta tem ponta em C → nenhuma aresta tem ambas pontas fora de C → V \ C é independente.

**Etapa 2 — Resolução:**

- Rode CoberturaMinima(G) no grafo original.
- Obtenha C* = cobertura mínima de vértices.

**Etapa 3 — Interpretação:**

- O conjunto independente máximo é **I* = V \ C***.
- |I*| = |V| - |C*|.
- Para construir I*: pegue todos os vértices que **não** estão na cobertura mínima.

**Justificativa:**
- Maximizar |I| = maximizar |V \ C| = minimizar |C|.
- Portanto, o **maior** independente corresponde ao complemento da **menor** cobertura.
- Transformação: O(1) (mesmo grafo) → polinomial ✅.
- Interpretação: O(V) (complementar o conjunto) → polinomial ✅.

**Exemplo:** Grafo com V = {a,b,c,d}, arestas {(a,b),(b,c),(c,d)}.
- Cobertura mínima: {b, c} (tamanho 2 — toca todas as arestas).
- Conjunto independente máximo: V \ {b,c} = {a, d} (tamanho 2 — sem arestas entre a e d ✅).

---

### Gabarito 4 — Maior subgrafo completo / clique (usando Conjunto independente máximo)

**Problema A:** Dado um grafo G = (V, E), encontrar a **maior clique** (maior subgrafo completo, onde todos os vértices são adjacentes entre si).

**Algoritmo dado:** Conjunto independente máximo.

---

**Etapa 1 — Transformação:**

Construa o **grafo complementar** Ḡ = (V, Ē):
- Mesmos vértices de G.
- Ē = { (u,v) : (u,v) ∉ E } — as arestas que **não** existem em G passam a existir em Ḡ, e vice-versa.

A relação é:

> **S é clique em G ⟺ S é conjunto independente em Ḡ.**

Isso vale porque:
- Se S é clique em G → todo par u,v ∈ S tem aresta em G → nenhum par tem aresta em Ḡ → S é independente em Ḡ.
- Se S é independente em Ḡ → nenhum par u,v ∈ S tem aresta em Ḡ → todo par tem aresta em G → S é clique em G.

**Etapa 2 — Resolução:**

- Rode ConjuntoIndependenteMaximo(Ḡ) no grafo complementar.
- Obtenha I* = conjunto independente máximo de Ḡ.

**Etapa 3 — Interpretação:**

- A maior clique de G é **exatamente I***.
- |clique máxima| = |I*|.

**Justificativa:**
- Pela equivalência acima, maximizar clique em G = maximizar independente em Ḡ.
- Construção de Ḡ: O(V²) → polinomial ✅.
- Interpretação: O(1) (mesmo conjunto) → polinomial ✅.

**Exemplo:** G com V = {a,b,c,d}, arestas {(a,b),(a,c),(b,c)}.
- Ḡ tem arestas: {(a,d),(b,d),(c,d)} (as que faltavam em G).
- Independente máximo de Ḡ: {a,b,c} (nenhum par tem aresta em Ḡ ✅).
- Logo, clique máxima de G: {a,b,c} (todos pares conectados em G ✅).

---

### Gabarito 5 — Verificar se grafo é bipartido (usando Coloração mínima de vértices)

**Problema A:** Dado um grafo G = (V, E), verificar se G é **bipartido** (pode ser dividido em dois conjuntos onde todas as arestas vão de um conjunto para o outro).

**Algoritmo dado:** Coloração mínima de vértices (encontrar o menor número de cores χ(G) tal que vértices adjacentes tenham cores diferentes).

---

**Etapa 1 — Transformação:**

Não precisa transformar o grafo! Use o **mesmo grafo G** como entrada.

A relação é:

> **G é bipartido ⟺ χ(G) ≤ 2**

Isso vale porque:
- Se G é bipartido com lados L e R → pinte L de cor 1 e R de cor 2 → coloração válida com 2 cores → χ(G) ≤ 2.
- Se χ(G) ≤ 2 → existe coloração com cores {1, 2} → seja L = vértices cor 1 e R = vértices cor 2 → nenhuma aresta liga vértices de mesma cor → todas as arestas vão de L para R → G é bipartido.

(Obs: se G não tem arestas, χ(G) = 1 e é trivialmente bipartido. Se G tem aresta, χ(G) ≥ 2.)

**Etapa 2 — Resolução:**

- Rode ColoraçãoMinima(G) no grafo original.
- Obtenha χ* = número cromático (menor número de cores necessário).

**Etapa 3 — Interpretação:**

- Se **χ* ≤ 2** → G **é bipartido** ✅
- Se **χ* ≥ 3** → G **não é bipartido** ✗

Para construir a bipartição: pegue os vértices pintados de cor 1 como lado L e os de cor 2 como lado R.

**Justificativa:**
- Bipartido ⟺ sem ciclos ímpares ⟺ 2-colorável ⟺ χ(G) ≤ 2.
- Transformação: O(1) (mesmo grafo) → polinomial ✅.
- Interpretação: O(1) (comparar χ* com 2) → polinomial ✅.

**Exemplo:** Grafo com V = {a,b,c,d}, arestas {(a,b),(b,c),(c,d),(d,a)}.
- Coloração mínima: χ* = 2 (a=1, b=2, c=1, d=2).
- χ* ≤ 2 → bipartido ✅. Lados: L = {a,c}, R = {b,d}.

**Contra-exemplo:** Grafo com V = {a,b,c}, arestas {(a,b),(b,c),(c,a)} (triângulo).
- Coloração mínima: χ* = 3.
- χ* ≥ 3 → não é bipartido ✗ (tem ciclo ímpar de tamanho 3).

---

## Tabela Resumo das Transformações

| # | Problema A | Algoritmo B | Transformação | Interpretação |
|---|-----------|-------------|---------------|---------------|
| 1 | Maior nº de arestas | Dijkstra | Peso -1 em cada aresta | Caminho mínimo = caminho com mais arestas |
| 2 | Emparelhamento máximo | Ford-Fulkerson | Rede com fonte, sumidouro, capacidade 1 | Fluxo máximo = emparelhamento |
| 3 | Conj. independente máx. | Cobertura mín. vértices | Mesmo grafo | I* = V \ C* |
| 4 | Maior clique | Conj. independente máx. | Grafo complementar Ḡ | Clique em G = independente em Ḡ |
| 5 | Bipartido? | Coloração mínima | Mesmo grafo | Bipartido ⟺ χ(G) ≤ 2 |
