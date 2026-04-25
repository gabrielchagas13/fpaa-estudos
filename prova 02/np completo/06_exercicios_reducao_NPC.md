# Exercícios — Redução e NP-Completo (CLRS 34.3 e 34.5)

**Disciplina:** Fundamentos de Projeto e Análise de Algoritmos · PUC Minas  

---

## Exercícios

### Ex. 1
Explique, com suas palavras, por que o Teorema de Cook-Levin é considerado o resultado mais importante da teoria de NP-completude.

### Ex. 2
Verdadeiro ou Falso: "Para provar que um problema B é NP-Completo, devo reduzir B a um problema NP-C conhecido." Justifique.

### Ex. 3
Verdadeiro ou Falso: "Se A ≤ₚ B e B ∈ P, então A ∈ P." Justifique.

### Ex. 4
Verdadeiro ou Falso: "Se A ≤ₚ B e A ∈ NP-Completo, então B ∈ NP-Completo." Justifique.

### Ex. 5
Explique a diferença entre NP-Difícil e NP-Completo. Dê um exemplo de problema NP-Difícil que (provavelmente) não é NP-Completo.

### Ex. 6
Descreva a redução de CLIQUE para COBERTURA DE VÉRTICES. Dado um grafo G com 5 vértices {a, b, c, d, e} e arestas {(a,b), (a,c), (b,c), (d,e)}, e k = 3, construa a instância de Cobertura de Vértices resultante da redução.

### Ex. 7
Descreva a redução de CICLO HAMILTONIANO para TSP. Explique por que essa redução é correta.

### Ex. 8
Liste 3 razões pelas quais a maioria dos pesquisadores acredita que P ≠ NP, mesmo sem prova formal.

### Ex. 9
Se amanhã alguém provar que P = NP, o que aconteceria com a criptografia RSA? Justifique usando o conceito de fatoração e NP-completude.

### Ex. 10
O Teorema de Ladner diz que, se P ≠ NP, existem problemas "intermediários" em NP — nem em P, nem NP-C. Cite dois candidatos a problemas intermediários e explique por quê.

### Ex. 11
Prove que a relação ≤ₚ é transitiva. Ou seja, se L₁ ≤ₚ L₂ e L₂ ≤ₚ L₃, então L₁ ≤ₚ L₃.

### Ex. 12
Explique por que a **direção** da redução importa. Se você quer provar que CLIQUE é NP-Completo, por que reduz 3-SAT → CLIQUE e não CLIQUE → 3-SAT?

### Ex. 13
Na cadeia de reduções do CLRS, explique por que é suficiente reduzir apenas um problema NP-C conhecido para provar que um novo é NP-C, em vez de precisar reduzir todos os problemas de NP.

### Ex. 14
Verdadeiro ou Falso: "Todo problema em P é NP-Completo." Justifique.

### Ex. 15
Considere o problema: "Dado grafo G e inteiro k, G tem conjunto independente de tamanho ≥ k?" Prove que é NP-Completo usando redução a partir de CLIQUE.

---
---
---

# GABARITO

---

### G1 — Importância do Teorema de Cook-Levin

O Teorema de Cook-Levin **resolveu o problema do ovo e da galinha**. Para provar que qualquer problema é NP-C, precisamos reduzir um NP-C já conhecido a ele. Mas o primeiro NP-C não tinha anterior para usar. Cook-Levin provou que SAT é NP-C **diretamente**, mostrando que qualquer problema em NP pode ser convertido em SAT (qualquer verificador → circuito → fórmula booleana). Isso criou a base sobre a qual todos os 8000+ problemas NP-C conhecidos foram provados por cadeia de reduções.

---

### G2 — Direção da redução

**FALSO.** A direção é o contrário: para provar que B é NP-C, devo reduzir um NP-C já conhecido **A para B** (A ≤ₚ B), e não B para A. Isso mostra que B é **pelo menos tão difícil** quanto A. Se reduzisse B para A, estaria mostrando que B é no máximo tão difícil quanto A — o que não prova nada sobre B ser NP-C.

---

### G3 — Preservação de tratabilidade

**VERDADEIRO.** Se A ≤ₚ B, existe f polinomial tal que x ∈ A ⟺ f(x) ∈ B. Se B ∈ P, existe algoritmo polinomial para B. Para resolver A: (1) aplica f em x (polinomial), (2) roda algoritmo de B em f(x) (polinomial). Composição de polinomiais = polinomial → A ∈ P.

---

### G4 — Herança de NP-completude

**FALSO (como está escrito).** Se A ≤ₚ B e A é NP-C, sabemos que B é **NP-Difícil** (pelo menos tão difícil quanto A). Mas para B ser NP-**Completo**, precisamos também que B ∈ NP. A redução sozinha não garante isso — B poderia ser NP-Difícil mas estar fora de NP. Logo está incompleta: falta verificar B ∈ NP.

---

### G5 — NP-Difícil vs NP-Completo

**NP-Difícil:** Todo problema em NP se reduz a ele. Não precisa estar em NP.

**NP-Completo:** Todo problema em NP se reduz a ele **E** ele está em NP.

NP-Completo = NP-Difícil ∩ NP.

**Exemplo NP-Difícil mas não NP-C:** O **Halting Problem** (problema da parada). Todo problema em NP se reduz a ele, mas é **indecidível** — não pode ser resolvido por nenhum algoritmo, muito menos verificado em tempo polinomial. Logo não está em NP.

Outro exemplo: versão de **otimização** do TSP ("qual é o tour mínimo?"). A resposta não é SIM/NÃO, não é problema de decisão, não está em NP na definição formal.

---

### G6 — Redução CLIQUE → Cobertura de Vértices (com exemplo)

**Redução:** Dado (G, k), construir (Ḡ, |V| - k) onde Ḡ é o grafo complementar.

**Aplicação:**

G: vértices {a,b,c,d,e}, arestas {(a,b),(a,c),(b,c),(d,e)}, k = 3.

Arestas do complemento Ḡ (as que NÃO estão em G):
- Ḡ tem arestas: {(a,d), (a,e), (b,d), (b,e), (c,d), (c,e)}

Instância de Cobertura: (Ḡ, |V| - k) = (Ḡ, 5 - 3) = (Ḡ, 2)

Pergunta: "Ḡ tem cobertura de vértices de tamanho ≤ 2?"

Verificação: {a,b,c} é clique em G (todos pares conectados ✅). Logo {d,e} = V \ {a,b,c} é cobertura de Ḡ:
- (a,d) → d ✅
- (a,e) → e ✅
- (b,d) → d ✅
- (b,e) → e ✅
- (c,d) → d ✅
- (c,e) → e ✅

Cobertura de tamanho 2 ✅. Resposta coincide.

---

### G7 — Redução Hamiltoniano → TSP

**Construção:** Dado G = (V, E):
- Cria grafo completo H, mesmos vértices
- w(u,v) = 1 se (u,v) ∈ E; w(u,v) = 2 se (u,v) ∉ E
- k = |V|

**Corretude (→):** Se G tem hamiltoniano → ciclo usa |V| arestas, todas em E, todas peso 1 → total = |V| = k ✅

**Corretude (←):** Se H tem tour peso ≤ |V| → tour tem |V| arestas, para total = |V| todas devem ter peso 1 → todas em E → formam hamiltoniano em G ✅

**Tempo:** O(V²) para construir H → polinomial ✅

---

### G8 — Por que se acredita P ≠ NP

1. **50+ anos de fracasso:** Milhares de pesquisadores tentaram e nenhum achou algoritmo polinomial pra qualquer NP-C. Evidência fortíssima.

2. **Assimetria natural:** Verificar é mais fácil que resolver. Montar quebra-cabeça vs checar se está montado. Se P = NP, essa assimetria não existiria.

3. **Consequências absurdas:** Se P = NP, toda criptografia quebraria, IA resolveria qualquer problema. Improvável demais.

---

### G9 — P = NP e RSA

RSA depende da dificuldade de **fatorar** números grandes. Fatoração está em NP ∩ co-NP. Se P = NP → todo problema em NP tem solução polinomial → fatoração (que é "mais fácil" que NP-C) certamente estaria em P → fatorar números grandes seria rápido → chaves RSA quebráveis → criptografia RSA insegura.

---

### G10 — Problemas intermediários (Ladner)

**Isomorfismo de grafos:** ∈ NP (certificado = bijeção). Babai (2015) → quase-polinomial. Provavelmente não é NP-C (ninguém conseguiu reduzir NP-C a ele) nem P (ninguém achou polinomial exato).

**Fatoração de inteiros:** ∈ NP ∩ co-NP. Se fosse NP-C → provar P=NP quebraria RSA. Se fosse P → RSA quebraria agora. Provavelmente intermediário. (Computadores quânticos resolveriam com Shor.)

---

### G11 — Transitividade de ≤ₚ

**Prova:** Sejam f e g funções de redução:
- f reduz L₁ a L₂: x ∈ L₁ ⟺ f(x) ∈ L₂, f é O(nᵏ)
- g reduz L₂ a L₃: y ∈ L₂ ⟺ g(y) ∈ L₃, g é O(nᶜ)

Defina h(x) = g(f(x)).

Corretude: x ∈ L₁ ⟺ f(x) ∈ L₂ ⟺ g(f(x)) ∈ L₃ ⟺ h(x) ∈ L₃ ✅

Tempo: f produz saída O(nᵏ). g roda em O(mᶜ) onde m = O(nᵏ). Total: O((nᵏ)ᶜ) = O(n^(kc)) → polinomial ✅

Logo L₁ ≤ₚ L₃. ∎

---

### G12 — Direção da redução

Para provar CLIQUE é NP-C, preciso mostrar que CLIQUE é **pelo menos tão difícil** quanto um NP-C conhecido (3-SAT).

3-SAT **→** CLIQUE significa: "se sei resolver CLIQUE, consigo resolver 3-SAT." Logo CLIQUE ≥ 3-SAT em dificuldade → CLIQUE é NP-Difícil ✅.

Se fizesse CLIQUE **→** 3-SAT, mostraria que 3-SAT ≥ CLIQUE — não prova nada sobre CLIQUE ser NP-C.

**Resumo:** seta vai DO difícil conhecido PARA o novo candidato.

---

### G13 — Basta um NP-C, não todos

Pela **transitividade** de ≤ₚ. Se L' é NP-C → todo problema em NP se reduz a L'. Se L' ≤ₚ L → por transitividade, todo problema em NP se reduz a L. L' já "concentra" toda a dificuldade de NP, então basta mostrar que L é tão difícil quanto L'.

---

### G14 — Todo P é NP-Completo?

**FALSO.** Problemas em P estão em NP (P ⊆ NP), mas **não são NP-Difíceis** (assumindo P ≠ NP). Se um problema em P fosse NP-C, como tem solução polinomial → P = NP. Contradiz a conjectura.

---

### G15 — Conjunto Independente é NP-C

**Passo 1 — ∈ NP:**
Certificado: conjunto S de k vértices. Verificação: checar que nenhum par em S é adjacente → O(k²) ⊆ O(V²) → polinomial ✅.

**Passo 2 — Redução de CLIQUE:**
Dado (G, k) instância de CLIQUE, construir (Ḡ, k) instância de INDEPENDENTE, onde Ḡ = complemento de G.

**Corretude:** S é clique em G ⟺ S é conjunto independente em Ḡ.

(→) S clique em G → todo par u,v ∈ S tem aresta em G → nenhum par tem aresta em Ḡ → S é independente em Ḡ ✅

(←) S independente em Ḡ → nenhum par u,v ∈ S tem aresta em Ḡ → todo par tem aresta em G → S é clique em G ✅

**Tempo:** Construir Ḡ → O(V²) → polinomial ✅

CLIQUE é NP-C e CLIQUE ≤ₚ INDEPENDENTE, e INDEPENDENTE ∈ NP → **INDEPENDENTE é NP-Completo**. ∎
