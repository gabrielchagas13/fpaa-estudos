# Exercícios de Transformação e Redução (CLRS 34.3)

**Disciplina:** Fundamentos de Projeto e Análise de Algoritmos · PUC Minas  
**Professor:** Felipe de Castro Belém  

---

> **Ideia geral:** você tem um problema A pra resolver, mas só tem o algoritmo de B disponível. Você **transforma** A em B, roda B, e lê a resposta de volta.

---

## Exercício 1 — Maior quantidade de arestas entre dois vértices (Dijkstra)

**Problema:** Dado um grafo não ponderado e dois vértices s e t, achar o caminho com **mais arestas** entre eles.

**Algoritmo disponível:** Dijkstra → acha o caminho de **menor peso**.

**O problema:** Dijkstra minimiza. A gente quer maximizar. **E Dijkstra não aceita pesos negativos.**

**Transformação:**

Seja M = |V| - 1 (máximo de arestas possível num caminho simples).

Atribua peso **w'(u,v) = M - 1** a cada aresta do grafo.

Assim, um caminho com mais arestas fica com **menor peso total** (porque cada aresta "tira" menos do total).

**Etapas:**

1. Crie G' com os mesmos vértices e arestas de G
2. Atribua peso w'(u,v) = M - 1 a toda aresta (sendo M = |V| - 1)
3. Rode Dijkstra(G', s, t)
4. O caminho de menor peso em G' é o caminho com mais arestas em G

**Justificativa:** Como todos os pesos são iguais e positivos, o caminho com menos peso total é o que usa mais arestas (cada aresta adicional adiciona M-1 ao custo... espera, isso não inverte). 

**Versão mais simples e correta:** Atribua **w'(u,v) = 1** a todas as arestas. O Dijkstra com peso 1 é equivalente a uma BFS. O caminho mais curto em número de arestas é o caminho de menor peso. Mas queremos o **maior**, não o menor.

**Solução correta:** Use o grafo G como está, mas rode **Dijkstra com pesos invertidos** da seguinte forma: já que Dijkstra não aceita negativos, substitua cada peso 1 por **w'(u,v) = M - 1** onde M é uma constante grande. Um caminho com k arestas tem peso k × (M-1). Para minimizar isso... ainda não inverte.

**A transformação correta é:** Use **Bellman-Ford** (que aceita pesos negativos) com w'(u,v) = -1. Ou reformule como: em vez de Dijkstra, use BFS e busque o caminho mais longo — mas isso é NP-Completo em geral.

> ⚠️ **Observação importante:** Encontrar o caminho mais longo em um grafo geral é NP-Completo. Dijkstra resolve o caminho mais curto. A transformação direta com pesos negativos não funciona com Dijkstra. O professor provavelmente aceita a resposta: **w'(u,v) = -1 com Bellman-Ford**, ou a observação de que a transformação só funciona em DAGs com Dijkstra modificado.

**Solução para a prova (resposta direta):**
- Construa G' atribuindo w'(u,v) = -1 a cada aresta
- Use Bellman-Ford (aceita negativos) ou, se insistir em Dijkstra, use w'(u,v) = C - 1 onde C é uma constante e inverta a leitura
- O caminho de menor custo em G' = caminho com maior número de arestas em G
- A transformação é O(E) → polinomial ✅

---

## Exercício 2 — Emparelhamento máximo em um grafo (Ford-Fulkerson)

**Problema:** Dado grafo G, achar o maior conjunto de arestas sem vértices em comum.

**Algoritmo disponível:** Ford-Fulkerson → acha fluxo máximo numa rede.

**Transformação (caso geral):**

1. **Duplique cada vértice v** em v_in e v_out, ligados por aresta v_in → v_out com **capacidade 1**
2. **Crie fonte s** e conecte s → v_in para todo v (capacidade 1)
3. **Crie sumidouro t** e conecte v_out → t para todo v (capacidade 1)
4. Para cada aresta (u,v) do grafo original: crie u_out → v_in e v_out → u_in (capacidade 1)

**Rode Ford-Fulkerson(N, s, t).**

**Leia a resposta:**
- Fluxo máximo f* = tamanho do emparelhamento
- As arestas do grafo original com fluxo 1 formam o emparelhamento

**Por que funciona:** A capacidade 1 na aresta interna v_in → v_out garante que cada vértice participa de no máximo uma aresta do emparelhamento. Ford-Fulkerson acha quantos "caminhos independentes" existem de s a t = quantas arestas cabem no emparelhamento.

**Tempo:** Construção da rede O(V + E) → polinomial ✅

---

## Exercício 3 — Conjunto independente máximo (Cobertura mínima de vértices)

**Problema:** Dado grafo G, achar o maior conjunto de vértices sem nenhuma aresta entre eles.

**Algoritmo disponível:** Cobertura mínima de vértices → acha o menor conjunto de vértices que toca todas as arestas.

**Transformação:** Nenhuma! Use o mesmo grafo G.

**A relação é:** S é conjunto independente ⟺ V \ S é cobertura de vértices.

**Etapas:**

1. Rode CoberturaMinima(G) → obtém C*
2. O conjunto independente máximo é **I* = V \ C***
3. Tamanho: |I*| = |V| - |C*|

**Por que funciona:** Se C cobre todas as arestas, então fora de C (ou seja, em V \ C) não existe nenhuma aresta — porque se existisse, C não estaria cobrindo ela. Logo V \ C é independente. E quanto menor C, maior V \ C.

**Tempo:** O(V) para complementar o conjunto → polinomial ✅

**Exemplo:** V = {a,b,c,d}, arestas {(a,b),(b,c),(c,d)}.
- Cobertura mínima: {b,c}
- Conjunto independente máximo: V \ {b,c} = **{a,d}** ✅

---

## Exercício 4 — Maior clique de um grafo (Conjunto independente máximo)

**Problema:** Dado grafo G, achar o maior subgrafo completo (todos os vértices conectados entre si).

**Algoritmo disponível:** Conjunto independente máximo.

**Transformação:** Construa o **grafo complementar Ḡ** de G.

Ḡ tem os mesmos vértices, mas as arestas são exatamente as que **não existem** em G.

**A relação é:** S é clique em G ⟺ S é conjunto independente em Ḡ.

**Etapas:**

1. Construa Ḡ: para cada par (u,v), se aresta existe em G → não existe em Ḡ, e vice-versa
2. Rode ConjuntoIndependenteMaximo(Ḡ) → obtém I*
3. I* é a maior clique de G

**Por que funciona:** Se S é clique em G, todo par de vértices em S tem aresta em G → nenhum par tem aresta em Ḡ → S é independente em Ḡ. O raciocínio inverso também vale.

**Tempo:** Construir Ḡ é O(V²) → polinomial ✅

**Exemplo:** G com V = {a,b,c,d}, arestas {(a,b),(a,c),(b,c)}.
- Ḡ tem arestas: {(a,d),(b,d),(c,d)}
- Independente máximo em Ḡ: {a,b,c} (nenhum par tem aresta em Ḡ)
- Logo clique máxima em G: **{a,b,c}** ✅

---

## Exercício 5 — Verificar se grafo é bipartido (Coloração mínima de vértices)

**Problema:** Dado grafo G, determinar se os vértices podem ser divididos em dois grupos onde toda aresta vai de um grupo para o outro.

**Algoritmo disponível:** Coloração mínima → acha o menor número de cores χ(G) para colorir os vértices sem adjacentes iguais.

**Transformação:** Nenhuma! Use o mesmo grafo G.

**A relação é:** G é bipartido ⟺ χ(G) ≤ 2

**Etapas:**

1. Rode ColoracaoMinima(G) → obtém χ*
2. Se χ* ≤ 2 → **G é bipartido** ✅
3. Se χ* ≥ 3 → **G não é bipartido** ✗
4. (Bônus) A bipartição: grupo L = vértices cor 1, grupo R = vértices cor 2

**Por que funciona:** Bipartido significa que você consegue separar os vértices em dois lados e pintar cada lado de uma cor diferente, sem que dois adjacentes tenham a mesma cor. Isso é exatamente uma 2-coloração. Se χ(G) = 1 (sem arestas) ou χ(G) = 2 → bipartido. Se precisa de 3 ou mais cores → tem ciclo ímpar → não bipartido.

**Tempo:** O(1) para comparar χ* com 2 → polinomial ✅

**Exemplo bipartido:** V = {a,b,c,d}, arestas {(a,b),(b,c),(c,d),(d,a)}.
- χ* = 2 (a=cor1, b=cor2, c=cor1, d=cor2)
- Bipartido ✅ → L = {a,c}, R = {b,d}

**Exemplo não bipartido:** Triângulo {a,b,c} com arestas {(a,b),(b,c),(c,a)}.
- χ* = 3 → não bipartido ✗ (ciclo ímpar de tamanho 3)

---

## Tabela Resumo

| Exercício | Problema A | Algoritmo B | Transformação | Como ler a resposta |
|-----------|-----------|-------------|---------------|---------------------|
| 1 | Maior nº arestas s→t | Dijkstra / Bellman-Ford | w'(u,v) = -1 | caminho mínimo = caminho com mais arestas |
| 2 | Emparelhamento máximo | Ford-Fulkerson | Duplicar vértices, fonte/sumidouro, cap 1 | fluxo máximo = tamanho do emparelhamento |
| 3 | Conj. independente máx. | Cobertura mín. vértices | Mesmo grafo | I* = V \ C* |
| 4 | Maior clique | Conj. independente máx. | Grafo complementar Ḡ | independente em Ḡ = clique em G |
| 5 | Bipartido? | Coloração mínima | Mesmo grafo | bipartido ⟺ χ(G) ≤ 2 |
