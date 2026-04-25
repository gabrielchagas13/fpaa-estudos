# Resumo — Transformação, Redução e NP-Completo (CLRS 34.3 e 34.5)

**Aluno:** Gabriel Chagas · 5º período · Eng. Software · PUC Minas  
**Disciplina:** Fundamentos de Projeto e Análise de Algoritmos  
**Professor:** Felipe de Castro Belém  

---

## Referências

- **Livro:** CORMEN, T. H. et al. *Algoritmos: Teoria e Prática*, 3ª ed. Capítulos 34.3 e 34.5  
- **Repo:** [joaopauloaramuni - FPAA (GitHub)](https://github.com/joaopauloaramuni/fundamentos-de-projeto-e-analise-de-algoritmos)  

### Vídeos no YouTube

| Vídeo | Descrição |
|-------|-----------|
| [P vs NP: A Questão que Pode Mudar a Computação](https://www.youtube.com/watch?v=GSJ58-Mz0bI) | Visão geral de P vs NP |
| [Classes P, NP, NP-completo, Redução](https://www.youtube.com/watch?v=ApRmVUOOY_o) | Reduções e provas, mais avançado |
| [NP-difícil e NP-Completo: SAT, CLIQUE, Cobertura](https://www.youtube.com/watch?v=aFkw--yDyHY) | Reduções passo a passo |
| [Univesp — Aula 14 — P, NP e NP-completos](https://www.youtube.com/watch?v=wsvXnmUHJX8) | Aula completa e didática |

---

# REDUÇÃO POLINOMIAL (CLRS 34.3)

## 1. O que é Redução?

Redução é **transformar** um problema A num problema B, de forma que resolver B te dá a resposta de A automaticamente.

**Exemplo do mundo real:** Você não sabe cozinhar lasanha, mas sabe seguir receita. Seu amigo te dá uma receita em inglês. Você não fala inglês, mas sabe usar o Google Tradutor.

Você **reduz** o problema:
1. Traduz a receita pro português (transformação → tempo polinomial)
2. Segue a receita em português (resolve o problema B)
3. A lasanha fica pronta (resposta de A)

Se a tradução é rápida, cozinhar lasanha em inglês não é mais difícil que cozinhar em português.

---

## 2. Definição Formal

Dizemos que L₁ é **redutível em tempo polinomial** a L₂, escrito **L₁ ≤ₚ L₂**, se existe uma função f computável em tempo polinomial tal que:

> x ∈ L₁ **se e somente se** f(x) ∈ L₂

A função f é a **função de redução**. Transforma qualquer instância de L₁ em instância de L₂, **preservando a resposta**: SIM vira SIM, NÃO vira NÃO.

```
  Instância de A ──[ f (tempo polinomial) ]──► Instância de B
       │                                            │
   Resposta: SIM  ◄─────── se e somente se ────────► Resposta: SIM
   Resposta: NÃO  ◄─────── se e somente se ────────► Resposta: NÃO
```

---

## 3. O que a Redução Significa

Quando dizemos **A ≤ₚ B**:

- **B é pelo menos tão difícil quanto A** — se você resolve B, resolve A também
- Se B ∈ P → A ∈ P
- Se A ∉ P → B ∉ P (contrapositiva)

**CUIDADO COM A DIREÇÃO!** A ≤ₚ B **NÃO** quer dizer que A é mais difícil. Quer dizer que A é **no máximo** tão difícil quanto B. Quem é "mais difícil" é o **B**.

---

## 4. Propriedades da Redução

**Transitiva:** Se A ≤ₚ B e B ≤ₚ C, então A ≤ₚ C. (Polinomial de polinomial = polinomial.)

**Não é simétrica:** A ≤ₚ B **NÃO** implica B ≤ₚ A.

**Reflexiva:** A ≤ₚ A (função identidade f(x) = x).

---

## 5. NP-Difícil e NP-Completo

**NP-Difícil:** Um problema L é NP-Difícil se **todo** problema em NP é redutível a L em tempo polinomial. L não precisa estar em NP — pode ser ainda mais difícil!

**NP-Completo (NPC):** Um problema L é NP-Completo se:

> 1. L ∈ NP
> 2. L é NP-Difícil

NP-Completo = está em NP **E** é o mais difícil possível dentro de NP.

```
┌──────────────────────────────────────────────┐
│                    NP                         │
│                                               │
│   ┌──────────┐        ┌──────────────────┐   │
│   │    P     │        │   NP-Completo    │   │
│   └──────────┘        └──────────────────┘   │
└──────────────────────────────────────────────┘
                         │
               ┌─────────┴──────────┐
               │   NP-Difícil       │  ← pode estar FORA de NP
               └────────────────────┘
```

---

## 6. O Teorema Central

> **Se qualquer problema NP-Completo pode ser resolvido em tempo polinomial, então P = NP.**

Porque: se L é NP-C e L ∈ P → todo problema em NP se reduz a L (NP-C) → composição polinomial resolve tudo → P = NP. ∎

---

## 7. Como Provar que um Problema é NP-Completo

**Passo 1:** Mostrar que está em **NP** (certificado + verificador polinomial).

**Passo 2:** Escolher um problema **já NP-C** (3-SAT, CLIQUE, etc).

**Passo 3:** Reduzir o NP-C conhecido **PARA** o novo problema. Mostrar:
- Transformação roda em tempo polinomial
- Resposta é preservada (SIM ↔ SIM, NÃO ↔ NÃO)

**DIREÇÃO:** DO conhecido PARA o novo. "Sei que X é difícil. Se X se transforma em Y, Y é pelo menos tão difícil."

---

# A IMPORTÂNCIA DO PRIMEIRO NP-COMPLETO

## 8. O Problema do Ovo e da Galinha

Para provar que B é NP-C, preciso reduzir um NP-C já conhecido a B. Mas o primeiro NP-C não tinha nenhum anterior para usar...

---

## 9. Teorema de Cook-Levin (1971)

Stephen Cook (e Leonid Levin) provaram que **SAT é NP-Completo sem usar redução de outro NP-C**.

A ideia:
- Todo problema em NP tem um verificador polinomial
- Todo verificador pode ser simulado por um computador
- Todo computador pode ser simulado por um circuito booleano
- Todo circuito pode ser convertido em fórmula booleana

Logo qualquer problema em NP se transforma em SAT → SAT é NP-Difícil. Como SAT ∈ NP → SAT é NP-Completo. ∎

**Importância:** Quebrou o ovo e a galinha. Depois de SAT, todos os outros NP-C são provados por cadeia de reduções:

```
SAT (Cook-Levin, 1971)
 └──► 3-SAT
       ├──► CLIQUE
       │     └──► COBERTURA DE VÉRTICES
       │           └──► CICLO HAMILTONIANO
       │                 └──► TSP
       ├──► CONJUNTO INDEPENDENTE
       └──► SUBSET SUM
              └──► PARTIÇÃO
                    └──► MOCHILA
```

---

# POR QUE P = NP NÃO FOI PROVADO NEM REFUTADO?

## 10. O Estado Atual

Ninguém provou P = NP. Ninguém provou P ≠ NP. Aberto desde 1971, vale **US$ 1.000.000** (Instituto Clay).

---

## 11. Por que é tão difícil provar P ≠ NP?

**1. Provar um negativo universal.** Não basta mostrar que os algoritmos conhecidos são lentos. Precisa provar que **nenhum** dos infinitos algoritmos possíveis funciona.

**2. Barreiras matemáticas.** Resultados de Baker-Gill-Solovay (1975) e Razborov-Rudich (1997) mostram que certas técnicas de prova **nunca** vão conseguir resolver P vs NP. Seria necessário inventar matemática nova.

**3. Relativização.** Existem "universos" onde P = NP e outros onde P ≠ NP. Qualquer prova precisa usar propriedades muito específicas da computação.

---

## 12. Por que é tão difícil provar P = NP?

Bastaria achar **um** algoritmo polinomial para **um** problema NP-C. Milhares de pesquisadores tentaram por 50+ anos e ninguém conseguiu.

---

## 13. O que a maioria acredita?

**P ≠ NP** (mais de 80% dos teóricos). Mas crença não é prova.

**Se P = NP:** criptografia quebraria, IA resolveria tudo, maior revolução da história da computação.

**Se P ≠ NP (provável):** criptografia segura, NP-C exigem heurísticas, distinção "verificar vs resolver" é permanente.

---

# PROBLEMAS EM P E NP AO MESMO TEMPO

## 14. Todo problema em P está em NP

Sim. P ⊆ NP. Se resolve rápido, verifica rápido (resolve e compara).

Exemplos: ordenação, busca, caminho mais curto, Euler, 2-SAT, 2-coloração, primalidade, programação linear...

---

## 15. Existem problemas em NP que NÃO estão em P?

Essa **é** a pergunta P vs NP. Candidatos: SAT, 3-SAT, CLIQUE, Hamiltoniano, 3-coloração, TSP, Subset Sum...

---

## 16. Problemas "no limbo" (Teorema de Ladner)

Se P ≠ NP, existem problemas em NP que não são P **nem** NP-C. Candidatos:

- **Isomorfismo de grafos** — Babai (2015) mostrou algoritmo quase-polinomial. Provavelmente não é NP-C nem P.
- **Fatoração de inteiros** — se fosse NP-C, provar P=NP quebraria RSA. Se fosse P, RSA quebraria agora. Provavelmente intermediário.

---

# OS NP-COMPLETOS DO CLRS 34.5

## 17. A Cadeia de Reduções

```
CIRCUIT-SAT (34.3)
  └──► SAT (34.4)
        └──► 3-SAT (34.5)
              ├──► CLIQUE (34.5)
              │     └──► COBERTURA DE VÉRTICES (34.5)
              ├──► CICLO HAMILTONIANO (34.5)
              │     └──► TSP (34.5)
              └──► SUBSET SUM (34.5)
```

---

## 18. 3-SAT → CLIQUE

**Entrada:** φ = C₁ ∧ C₂ ∧ ... ∧ Cₖ, cada cláusula com 3 literais.

**Construção:**
- Para cada literal de cada cláusula, cria um vértice (3k vértices)
- Liga dois vértices se: (a) estão em cláusulas **diferentes** E (b) **não** são complementares (x e ¬x não se ligam)

**Vale:** φ satisfatível ⟺ G tem clique de tamanho k

**Por quê:** Se φ é satisfatível → pega um literal verdadeiro por cláusula → esses k vértices formam clique (cláusulas diferentes + compatíveis = todos ligados). Na volta, clique de tamanho k → um vértice por cláusula (mesma cláusula não se liga) → literais compatíveis → definem atribuição que satisfaz φ.

---

## 19. CLIQUE → COBERTURA DE VÉRTICES

**Redução:** Dado (G, k), construir (Ḡ, |V| - k) onde Ḡ é o complemento de G.

**Fato:** G tem clique de tamanho k ⟺ Ḡ tem cobertura de vértices de tamanho |V| - k

**Prova (→):** Se S é clique em G → V \ S cobre todas as arestas de Ḡ (qualquer aresta de Ḡ tem pelo menos uma ponta fora da clique).

**Prova (←):** Se C é cobertura em Ḡ → V \ C é clique em G (se u,v ∉ C, aresta (u,v) não pode estar em Ḡ, logo está em G).

---

## 20. HAMILTONIANO → TSP

**Construção:** Dado G = (V, E):
- Cria grafo completo H, mesmos vértices
- w(u,v) = 1 se (u,v) ∈ E; w(u,v) = 2 se (u,v) ∉ E
- k = |V|

**Vale:** G tem hamiltoniano ⟺ H tem tour com peso ≤ |V|

Se G tem hamiltoniano → todas as arestas com peso 1 → total = |V| ✅. Se não tem → precisa aresta peso 2 → total > |V| ✗.

---

## 21. 3-SAT → SUBSET SUM

Redução numérica. Para cada variável e cláusula, cria números com dígitos especiais que codificam a fórmula. A soma alvo é construída para que atingi-la ⟺ satisfazer todas as cláusulas.

---

## 22. Tabela Resumo dos NP-Completos

| Problema | Redução de | Certificado | Verificação |
|----------|-----------|-------------|-------------|
| CIRCUIT-SAT | Direto (Cook-Levin) | Valores das entradas | O(circuito) |
| SAT | CIRCUIT-SAT | Atribuição de valores | O(\|φ\|) |
| 3-SAT | SAT | Atribuição de valores | O(\|φ\|) |
| CLIQUE | 3-SAT | Conjunto de k vértices | O(k²) |
| COB. VÉRTICES | CLIQUE | Conjunto de ≤ k vértices | O(E) |
| HAMILTONIANO | COB. VÉRTICES | Sequência de vértices | O(V) |
| TSP | HAMILTONIANO | Ciclo com pesos | O(V) |
| SUBSET SUM | 3-SAT | Subconjunto | O(n) |

---

## 23. Contrastes que caem em prova

| Fácil (P) | Difícil (NP-Completo) |
|-----------|----------------------|
| Circuito de Euler (arestas) | Circuito Hamiltoniano (vértices) |
| 2-coloração | 3-coloração |
| 2-SAT | 3-SAT |
| Caminho mais curto | Caminho simples mais longo |
| Cobertura mín. de arestas | Cobertura mín. de vértices |
| Programação Linear | Programação Inteira |
| Emparelhamento | Clique máxima |
