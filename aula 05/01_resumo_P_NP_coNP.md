# Resumo — Classe P (CLRS 34.1) e Classe NP e co-NP (CLRS 34.2)

**Aluno:** Gabriel Chagas · 5º período · Eng. Software · PUC Minas  
**Disciplina:** Fundamentos de Projeto e Análise de Algoritmos  
**Professor:** Felipe de Castro Belém  

---

## Referências e Vídeos

- **Livro:** CORMEN, T. H. et al. *Algoritmos: Teoria e Prática*, 3ª ed. Capítulos 34.1 e 34.2  
  [PDF do livro](https://computerscience360.wordpress.com/wp-content/uploads/2018/02/algoritmos-teoria-e-prc3a1tica-3ed-thomas-cormen.pdf)  
- **Repo do outro professor:** [joaopauloaramuni - FPAA (GitHub)](https://github.com/joaopauloaramuni/fundamentos-de-projeto-e-analise-de-algoritmos)  

### Vídeos no YouTube

| Vídeo | Descrição |
|-------|-----------|
| [P vs NP: A Questão que Pode Mudar a Computação](https://www.youtube.com/watch?v=GSJ58-Mz0bI) | Visão geral de P vs NP em português, ótimo pra começar |
| [Univesp — Aula 14 — Problemas P, NP e NP-completos](https://www.youtube.com/watch?v=wsvXnmUHJX8) | Aula completa da Univesp, bem didática |
| [Classes P, NP, NP-completo, NP-difícil e Redução](https://www.youtube.com/watch?v=ApRmVUOOY_o) | Mostra reduções e provas, mais avançado |
| [NP-difícil e NP-Completo: SAT, CLIQUE, Cobertura](https://www.youtube.com/watch?v=aFkw--yDyHY) | Reduções de SAT a CLIQUE, Cobertura de Vértices etc |

---

# CAPÍTULO 34.1 — CLASSE P

## 1. Problemas de Decisão

Toda a teoria de complexidade trabalha com **problemas de decisão**: a resposta é sempre **SIM** ou **NÃO**.

Por que só SIM ou NÃO? Porque simplifica a análise teórica. Problemas de otimização ("qual o menor caminho?") sempre podem ser convertidos em versões de decisão ("existe caminho com peso ≤ k?").

**Exemplo do mundo real:**
- Otimização: "Qual a rota mais barata de BH pra SP pelo iFood?"
- Decisão: "Existe rota que custa ≤ R$ 10?" → SIM ou NÃO

---

## 2. Problemas de Decisão como Linguagens

O CLRS formaliza problemas de decisão como **linguagens**. A ideia é:

- Uma **instância** do problema é codificada como uma string binária (sequência de 0s e 1s).
- Um problema de decisão é visto como uma **linguagem** L ⊆ {0,1}* — o conjunto de todas as strings para as quais a resposta é SIM.
- Um algoritmo **aceita** uma string x se retorna 1 (SIM).
- Um algoritmo **rejeita** uma string x se retorna 0 (NÃO).
- Um algoritmo **decide** uma linguagem L se aceita toda string em L e rejeita toda string fora de L.

**Diferença crucial:**
- **Aceitar**: retorna 1 para strings em L, mas pode rodar para sempre para strings fora de L.
- **Decidir**: retorna 1 para strings em L e 0 para strings fora de L — **sempre para**.

Para a Classe P precisamos de algoritmos que **decidem** (sempre param em tempo polinomial).

---

## 3. Codificação da Entrada

A forma como você representa a entrada afeta o tamanho n e, portanto, se o algoritmo é "polinomial" ou não.

**Exemplo:** Um número inteiro k.
- Em **unário** (111...1, com k dígitos): tamanho n = k. Um algoritmo O(k) seria O(n) → polinomial.
- Em **binário** (representação normal): tamanho n = log₂(k). Um algoritmo O(k) seria O(2^n) → **exponencial**!

O CLRS assume codificação "razoável" (geralmente binária) e mostra que para codificações razoáveis, a Classe P não muda. Isso torna P uma classe **robusta**.

---

## 4. Definição de Tempo Polinomial

Um algoritmo roda em **tempo polinomial** se existe uma constante k tal que, para entradas de tamanho n, o tempo de execução é O(n^k).

| Tempo | Exemplo | Polinomial? |
|-------|---------|:-----------:|
| O(1) | Constante | ✅ Sim |
| O(log n) | Busca binária | ✅ Sim |
| O(n) | Busca linear | ✅ Sim |
| O(n log n) | Merge sort | ✅ Sim |
| O(n²) | Bubble sort | ✅ Sim |
| O(n³) | Floyd-Warshall | ✅ Sim |
| O(n^100) | Absurdo, mas... | ✅ Sim |
| O(2^n) | Força bruta | ❌ Não |
| O(n!) | Permutações | ❌ Não |

**A regra:** expoente é **constante** (n², n³) → polinomial. A variável n está no **expoente** (2^n, n!) → não é polinomial.

---

## 5. Definição Formal da Classe P

> **P** = { L ⊆ {0,1}* : existe um algoritmo A de tempo polinomial tal que, para todo x ∈ {0,1}*, A(x) = 1 ⟺ x ∈ L }

**Em português:** P é o conjunto de problemas de decisão (linguagens) que algum algoritmo consegue **decidir corretamente** em **tempo polinomial**.

---

## 6. Por que P é importante?

P é a classe dos problemas **tratáveis**. Três razões:

1. **Independência de máquina:** Se um problema está em P para uma máquina de Turing, está em P para qualquer computador razoável. Trocar de computador multiplica o tempo por fator polinomial, e polinomial × polinomial = polinomial.

2. **Fechamento por composição:** Se você tem dois algoritmos polinomiais e roda um dentro do outro, o resultado é polinomial. Isso permite construir soluções complexas a partir de peças simples.

3. **Tese de Cobham-Edmonds:** "Os problemas tratáveis são exatamente os que estão em P."

---

## 7. Exemplos de Problemas em P

| Problema | Algoritmo | Complexidade |
|----------|-----------|:------------:|
| Ordenação | Merge Sort | O(n log n) |
| Busca em grafo | BFS / DFS | O(V + E) |
| Caminho mais curto | Dijkstra | O(E + V log V) |
| Primalidade | AKS (2002) | O(log^6 n) |
| Circuito de Euler | Checar graus pares | O(V + E) |
| Árvore geradora mínima | Kruskal / Prim | O(E log V) |
| 2-coloração | BFS (bipartido?) | O(V + E) |
| 2-SAT | Comp. fortemente conexas | O(n + m) |
| Emparelhamento perfeito | Edmonds (Blossom) | O(V³) |
| Cobertura mín. de arestas | Matching + extensão | O(V³) |
| Programação Linear | Pontos interiores | Polinomial |

---

# CAPÍTULO 34.2 — CLASSE NP E co-NP

## 8. Verificação em Tempo Polinomial

A ideia central do 34.2 é separar **resolver** de **verificar**.

- **Resolver** = encontrar a resposta do zero.
- **Verificar** = dado um "palpite" (certificado), confirmar se está correto.

Muitos problemas são difíceis de resolver mas fáceis de verificar.

**Exemplo do mundo real — Quebra-cabeça de 5000 peças:**
- **Resolver** (montar do zero): pode levar horas/dias.
- **Verificar** (olhar um quebra-cabeça já montado e ver se está certo): minutos.

**Exemplo computacional — Ciclo Hamiltoniano:**
- **Resolver** (encontrar um ciclo que passe por todos os vértices): ninguém conhece algoritmo polinomial.
- **Verificar** (alguém te dá uma sequência de vértices e você checa): percorrer a lista, verificar que são todos os vértices sem repetição e que as arestas existem → O(V). Polinomial.

---

## 9. Certificado (Testemunha)

Um **certificado** (ou testemunha) é uma informação adicional que permite verificar a resposta de uma instância.

- **Certificado positivo:** prova que a resposta é SIM.
- **Certificado negativo:** prova que a resposta é NÃO.

O certificado precisa ter **tamanho polinomial** em relação ao tamanho da entrada (senão não dá pra ler em tempo polinomial).

**Exemplos de certificados positivos:**

| Problema | Certificado positivo | Verificação |
|----------|---------------------|-------------|
| "n é composto?" | Um divisor d, 1 < d < n | Checar d \| n → O(log² n) |
| "Grafo tem ciclo hamiltoniano?" | Sequência de vértices | Checar unicidade + arestas → O(V) |
| "Fórmula SAT é satisfatível?" | Atribuição de valores | Avaliar fórmula → O(\|φ\|) |
| "Grafo tem clique de tamanho k?" | Conjunto de k vértices | Checar todos os pares adjacentes → O(k²) |
| "Existe subconjunto com soma t?" | O subconjunto | Somar elementos → O(n) |

---

## 10. Definição Formal de Verificador

Um **algoritmo de verificação** é um algoritmo A de dois argumentos:
- A(x, y) onde x é a instância e y é o certificado.

A **verifica** a linguagem L se:
- Para todo x ∈ L, **existe** um certificado y tal que A(x, y) = 1.
- Para todo x ∉ L, **não existe** nenhum certificado y tal que A(x, y) = 1.

O certificado y deve ter tamanho |y| = O(|x|^c) para alguma constante c.

---

## 11. Definição Formal da Classe NP

> **NP** = { L ⊆ {0,1}* : existe um verificador A de tempo polinomial tal que L = { x ∈ {0,1}* : existe certificado y com |y| = O(|x|^c) e A(x,y) = 1 } }

**Em português:** NP é o conjunto de problemas cuja resposta **SIM** pode ser **verificada** em tempo polinomial, dado um certificado de tamanho polinomial.

**ATENÇÃO:** NP **não** significa "Não Polinomial"! Significa **Nondeterministic Polynomial** — polinomial em uma máquina de Turing não-determinística.

---

## 12. Definição Equivalente: Máquina de Turing Não-Determinística

Uma visão equivalente (que o CLRS menciona):

> Um problema está em NP se uma **máquina de Turing não-determinística** consegue resolvê-lo em tempo polinomial.

A máquina não-determinística pode "chutar" a resposta certa (o certificado) magicamente e depois verificar. Como a verificação é polinomial → o problema está em NP.

Na prática, essa definição é equivalente à do verificador. Use a que for mais intuitiva pra você.

---

## 13. P ⊆ NP

**Teorema:** Todo problema em P também está em NP.

**Prova:** Se L ∈ P, existe algoritmo polinomial A que decide L. Para verificar, use certificado vazio (y = ε): o verificador simplesmente roda A(x) e ignora y. Como A é polinomial, a verificação é polinomial. Logo L ∈ NP. ∎

**Intuitivamente:** Se você consegue resolver rápido, com certeza consegue verificar rápido (é mais fácil verificar do que resolver).

---

## 14. Classe co-NP

> **co-NP** = { L : o complemento L̄ está em NP }

Ou seja, co-NP é o conjunto dos problemas cuja resposta **NÃO** pode ser verificada em tempo polinomial, dado um **certificado negativo**.

**Exemplo — "n é primo?"**
- Certificado negativo (provar que NÃO é primo): fornecer um divisor d, 1 < d < n, que divide n. Verificação: uma divisão → O(log² n).
- O complemento "n é composto?" está em NP (certificado = divisor).
- Logo "n é primo?" está em co-NP.

**Exemplo — "Grafo NÃO tem ciclo hamiltoniano?"**
- Certificado negativo: ??? Não se conhece como provar eficientemente que um grafo NÃO tem ciclo hamiltoniano.
- Portanto, não sabemos se o problema do ciclo hamiltoniano está em co-NP.

---

## 15. P ⊆ co-NP

**Teorema:** Todo problema em P também está em co-NP.

**Prova:** Se L ∈ P, então L̄ (o complemento) também está em P (basta inverter a resposta do algoritmo). Como L̄ ∈ P ⊆ NP, então L ∈ co-NP. ∎

---

## 16. Relação P, NP e co-NP — Diagrama

```
              NP                         co-NP
           /      \                    /       \
          / NP-C    \                 /          \
         /           \               /            \
        |              |            |              |
        |      P  =  NP ∩ co-NP  (conjectura)     |
        |              |            |              |
         \           /               \            /
          \         /                 \          /
           \      /                    \       /
```

**Fatos confirmados:**
- P ⊆ NP
- P ⊆ co-NP
- P ⊆ NP ∩ co-NP

**Perguntas abertas (ninguém sabe):**
- P = NP?
- P = NP ∩ co-NP?
- NP = co-NP?

**Se P ≠ NP**, então NP ≠ co-NP e existem problemas em NP que não estão em co-NP (e vice-versa).

---

## 17. Regra Prática para Classificar na Prova

| Você encontrou... | Então o problema está em... |
|-------------------|---------------------------|
| Algoritmo polinomial que resolve | **P, NP e co-NP** |
| Certificado positivo verificável em tempo polinomial, mas sem algoritmo polinomial | **NP** (e talvez co-NP, mas precisa provar separadamente) |
| Certificado negativo verificável em tempo polinomial, mas sem algoritmo polinomial | **co-NP** (e talvez NP, mas precisa provar separadamente) |
| Ambos os certificados verificáveis em tempo polinomial | **NP ∩ co-NP** (e talvez P, mas precisa provar) |

**Dica pro Felipe:** Quando ele pede pra classificar, siga esse roteiro:
1. Escreva o **problema de decisão** (sempre com SIM/NÃO).
2. Tente achar um **algoritmo polinomial**. Se achar → P, NP e co-NP. Pronto.
3. Se não achar algoritmo, defina o **certificado positivo** e mostre que a verificação é polinomial → NP.
4. Defina o **certificado negativo** e tente mostrar verificação polinomial → co-NP.
5. Conclua.

---

## 18. Contrastes Clássicos que Caem em Prova

| Fácil (P) | Difícil (NP-Completo) |
|-----------|----------------------|
| Circuito de Euler (arestas) | Circuito Hamiltoniano (vértices) |
| 2-coloração | 3-coloração |
| 2-SAT | 3-SAT |
| Caminho mais curto | Caminho simples mais longo |
| Cobertura mín. de arestas | Cobertura mín. de vértices |
| Programação Linear | Programação Inteira |
| Emparelhamento | Clique máxima |

**Memorize esses pares.** O Felipe adora perguntar um e esperar que você saiba que o "primo" dele é o oposto.
