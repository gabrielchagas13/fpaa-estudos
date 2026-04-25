# Resumo — Transformação e Redução (CLRS 34.3)

**Aluno:** Gabriel Chagas · 5º período · Eng. Software · PUC Minas  
**Disciplina:** Fundamentos de Projeto e Análise de Algoritmos  
**Professor:** Felipe de Castro Belém  

---

## Referências

- **Livro:** CORMEN, T. H. et al. *Algoritmos: Teoria e Prática*, 3ª ed. Capítulo 34.3  
- **Repo:** [joaopauloaramuni - FPAA (GitHub)](https://github.com/joaopauloaramuni/fundamentos-de-projeto-e-analise-de-algoritmos)  

### Vídeos no YouTube

| Vídeo | Descrição |
|-------|-----------|
| [Classes P, NP, NP-completo, Redução](https://www.youtube.com/watch?v=ApRmVUOOY_o) | Reduções e provas passo a passo |
| [NP-difícil e NP-Completo: SAT, CLIQUE, Cobertura](https://www.youtube.com/watch?v=aFkw--yDyHY) | Reduções concretas entre problemas |
| [Univesp — Aula 14 — P, NP e NP-completos](https://www.youtube.com/watch?v=wsvXnmUHJX8) | Aula completa e didática |

---

## 1. O que é Redução?

Redução é **usar a solução de um problema B para resolver um problema A**. Você transforma a entrada de A numa entrada de B, roda o algoritmo de B, e interpreta a saída de volta pra A.

**Exemplo do mundo real — Uber:**

Você quer saber qual é o restaurante mais perto de você. Você não tem app de restaurante, mas tem o Uber com mapa.

1. **Transforma:** pega a lista de restaurantes e joga no mapa do Uber como destinos
2. **Resolve:** o Uber calcula a distância até cada destino
3. **Interpreta:** o destino mais perto = restaurante mais perto

Você **reduziu** "achar restaurante mais perto" ao problema "calcular distância no mapa", que o Uber já resolve.

---

## 2. Definição Formal

Dizemos que L₁ é **redutível em tempo polinomial** a L₂, escrito:

> **L₁ ≤ₚ L₂**

Se existe uma função f computável em tempo polinomial tal que:

> x ∈ L₁ **se e somente se** f(x) ∈ L₂

A função f é a **função de redução**. Ela transforma qualquer instância de L₁ em instância de L₂, **preservando a resposta**:

```
  Instância de A ──[ f (tempo polinomial) ]──► Instância de B
       │                                            │
   Resposta SIM  ◄────── se e somente se ──────────► Resposta SIM
   Resposta NÃO  ◄────── se e somente se ──────────► Resposta NÃO
```

**Três exigências:**
1. f transforma **toda** instância de A em instância de B (não pode falhar)
2. f preserva a resposta nos **dois sentidos** (SIM↔SIM e NÃO↔NÃO)
3. f roda em **tempo polinomial**

---

## 3. Cuidado com a Direção!

Quando escrevemos **A ≤ₚ B**, estamos dizendo:

- "A se reduz a B"
- "Eu uso B para resolver A"
- "B é **pelo menos tão difícil** quanto A"
- "A é **no máximo** tão difícil quanto B"

**Quem é mais difícil é o B**, não o A. O símbolo ≤ₚ aponta do mais fácil pro mais difícil.

**Analogia:** Se você transforma "somar 2+2" em "resolver integral tripla", a integral é mais difícil. A soma se reduz à integral (soma ≤ₚ integral), não o contrário.

**Erro comum na prova:** trocar a direção. Se quer provar que CLIQUE é NP-C, reduz 3-SAT **→** CLIQUE (do conhecido pro novo), e **não** CLIQUE → 3-SAT.

---

## 4. Consequências da Redução

Se **A ≤ₚ B**:

| Se você sabe que... | Então conclui que... |
|---------------------|---------------------|
| B ∈ P | A ∈ P (se o difícil é fácil, o fácil também é) |
| A ∉ P | B ∉ P (se o fácil é difícil, o difícil também é) |
| B ∈ NP | A ∈ NP |
| A é NP-C | B é NP-Difícil |

**Contrapositiva importante:** Se A ≤ₚ B e A ∉ P, então B ∉ P. Essa é a base para provar que problemas são difíceis — você mostra que um problema reconhecidamente difícil se transforma nele.

---

## 5. Propriedades da Relação ≤ₚ

**Reflexiva:** A ≤ₚ A. (Função identidade f(x) = x serve como redução trivial.)

**Transitiva:** Se A ≤ₚ B e B ≤ₚ C, então A ≤ₚ C.

*Prova:* Sejam f (reduz A a B, tempo O(nᵏ)) e g (reduz B a C, tempo O(nᶜ)). Defina h(x) = g(f(x)). Então x ∈ A ⟺ f(x) ∈ B ⟺ g(f(x)) ∈ C ⟺ h(x) ∈ C. Tempo: f produz saída O(nᵏ), g roda em O((nᵏ)ᶜ) = O(n^(kc)) → polinomial. ∎

**NÃO é simétrica:** A ≤ₚ B **não** implica B ≤ₚ A. Saber resolver B resolve A, mas saber resolver A não necessariamente resolve B.

---

## 6. Dois Tipos de Uso da Redução

### 6.1 — Redução para RESOLVER (transformação prática)

Você tem um problema A e um algoritmo que resolve B. Transforma A em B, roda o algoritmo, pega a resposta.

**Exemplo:** Quer achar a maior clique de G. Você tem um algoritmo de conjunto independente máximo. Transforma: constrói o complemento Ḡ. Roda: independente máximo de Ḡ. Interpreta: esse conjunto é a clique máxima de G.

Esse é o tipo que o Felipe pede nos exercícios de transformação (tipo "use Dijkstra para resolver X").

### 6.2 — Redução para PROVAR DIFICULDADE

Você quer provar que B é difícil. Pega um problema A que já sabe que é difícil e mostra que A se transforma em B. Conclusão: B é pelo menos tão difícil quanto A.

**Exemplo:** Quer provar que CLIQUE é NP-C. Pega 3-SAT (já NP-C) e mostra 3-SAT ≤ₚ CLIQUE. Conclusão: CLIQUE é NP-Difícil. Como CLIQUE ∈ NP → CLIQUE é NP-Completo.

---

## 7. Definição de NP-Difícil

> Um problema L é **NP-Difícil** se todo problema L' ∈ NP satisfaz L' ≤ₚ L.

Em português: L é pelo menos tão difícil quanto **qualquer** problema em NP.

L **não precisa estar em NP**. Pode ser ainda mais difícil (indecidível, por exemplo).

---

## 8. Definição de NP-Completo

> Um problema L é **NP-Completo** se:
> 1. L ∈ NP
> 2. L é NP-Difícil

NP-Completo = o **mais difícil possível** dentro de NP.

```
┌──────────────────────────────────────────┐
│                  NP                       │
│                                           │
│   ┌────────┐       ┌────────────────┐    │
│   │   P    │       │  NP-Completo   │    │
│   └────────┘       └────────────────┘    │
└──────────────────────────────────────────┘
                      │
            ┌─────────┴──────────┐
            │   NP-Difícil       │ ← pode estar FORA de NP
            │   (ex: Halting     │
            │    Problem)        │
            └────────────────────┘
```

---

## 9. O Teorema Central da NP-Completude

> **Se qualquer problema NP-Completo pode ser resolvido em tempo polinomial, então P = NP.**

**Prova:**
- Seja L NP-C com L ∈ P
- Todo L' ∈ NP tem L' ≤ₚ L (definição de NP-C)
- L ∈ P → existe algoritmo polinomial para L
- Composição: redução polinomial + solução polinomial = polinomial
- Logo todo L' ∈ NP está em P → P = NP ∎

**Contrapositiva:** Se P ≠ NP, então nenhum NP-C tem solução polinomial.

---

## 10. Como Provar que um Problema é NP-Completo

**Passo 1:** Mostrar que o problema **está em NP** (certificado + verificação polinomial).

**Passo 2:** Escolher um problema **já NP-C** (3-SAT, CLIQUE, Cobertura, Hamiltoniano...).

**Passo 3:** Fazer a **redução do NP-C conhecido PARA o novo**:
- Descrever a transformação f
- Mostrar que f roda em tempo polinomial
- Provar que x ∈ L_conhecido ⟺ f(x) ∈ L_novo (ambas direções!)

**Macete da direção:** "Eu sei que X é difícil. Se X se transforma em Y, então Y é pelo menos tão difícil." Seta: X **→** Y.

---

## 11. O Primeiro NP-Completo: Cook-Levin

Para provar o primeiro NP-C, não dá pra usar redução (não existe NP-C anterior). Cook e Levin (1971) provaram que **SAT é NP-Completo diretamente**:

- Qualquer problema em NP tem verificador polinomial
- Verificador → simulado por computador → simulado por circuito → convertido em fórmula booleana
- Logo qualquer problema em NP se transforma em SAT
- SAT ∈ NP (certificado = atribuição)
- Portanto SAT é NP-Completo ∎

Depois de SAT, todos os outros são provados em cadeia:

```
CIRCUIT-SAT → SAT → 3-SAT → CLIQUE → COBERTURA → HAMILTONIANO → TSP
                          └→ SUBSET SUM → PARTIÇÃO → MOCHILA
                          └→ CONJUNTO INDEPENDENTE
                          └→ 3-COLORAÇÃO
```

---

## 12. Exemplos de Reduções Clássicas

### CLIQUE → Cobertura de Vértices (por complemento)

Dado (G, k), construa (Ḡ, |V|-k). Clique em G ⟺ cobertura em Ḡ.

### CLIQUE → Conjunto Independente (por complemento)

Dado (G, k), construa (Ḡ, k). Clique em G ⟺ independente em Ḡ.

### Hamiltoniano → TSP (por pesos)

Dado G, construa grafo completo H: peso 1 se aresta ∈ G, peso 2 se não. Hamiltoniano ⟺ tour ≤ |V|.

### 3-SAT → CLIQUE (por gadgets)

Cada literal vira vértice, liga vértices de cláusulas diferentes que não se contradizem. Satisfatível ⟺ clique de tamanho k.

---

## 13. Reduções como Transformações Práticas

Na prova, o Felipe pede dois tipos de exercício:

**Tipo 1 — Classificar:** "Este problema é P, NP, co-NP?" → use certificados

**Tipo 2 — Transformar:** "Resolva o problema A usando o algoritmo B" → siga o roteiro:

1. **Entrada:** o que você recebe
2. **Transformação:** como converter instância de A em instância de B (descreva f)
3. **Resolução:** rode o algoritmo de B
4. **Interpretação:** como a saída de B responde A
5. **Justificativa:** por que funciona (SIM↔SIM, NÃO↔NÃO) e por que é polinomial

---

## 14. Tabela de Transformações Comuns

| Problema A | Resolvido via B | Transformação |
|-----------|----------------|---------------|
| Clique máxima | Independente máximo | Complemento Ḡ |
| Independente máximo | Cobertura mínima | I = V \ C |
| Cobertura mínima | Independente máximo | C = V \ I |
| Clique máxima | Cobertura mínima | Complemento Ḡ + C = V \ I |
| Bipartido? | Coloração mínima | Bipartido ⟺ χ(G) ≤ 2 |
| Caminho mais longo | Dijkstra | Pesos negativos (-1) |
| Emparelhamento máx. | Fluxo máximo | Rede com fonte/sumidouro, cap. 1 |
| Hamiltoniano | TSP | Grafo completo, pesos 1/2 |

---

## 15. O que o Felipe Cobra sobre 34.3

Olhando o estilo dele:

1. **Exercícios de transformação:** "Use o algoritmo X para resolver Y" — descreva passo a passo
2. **V/F sobre redução:** "Se A ≤ₚ B e B ∈ P, então A ∈ P" — justifique
3. **Direção:** ele pode perguntar "por que reduzimos A para B e não B para A?"
4. **Provar NP-C:** possivelmente pedir que você prove um problema NP-C por redução

**Dicas:**
- Sempre justifique a direção da redução
- Sempre mostre que a transformação é polinomial
- Sempre prove as duas direções (SIM→SIM e NÃO→NÃO)
- Na dúvida, use 3-SAT como ponto de partida (é o "canivete suíço" das reduções)
