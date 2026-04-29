
---

> **Observação:** Não anexarei a foto da prova, mas considere que este conteúdo corresponde fielmente a uma prova anterior aplicada pelo professor.

---

# Prova 1 – 1/2026

**Fundamentos de Projeto e Análise de Algoritmos**
**PUC Minas**

---

## Questão 01 (10% cada)

Verifique se as afirmações são verdadeiras ou falsas. **Explique brevemente** sua resposta.

a) A complexidade ( O(n) + O(m) ) é de ( O(\max(n, m)) ).

b) ( 3n^2 + 2n - 1 \in O(n^3) ).

c) Se ( f(n) \in \Theta(g(n)) ) então ( g(n) \in \Theta(f(n)) ).

---

## Questão 02 (15%)

Escreva um trecho de código cuja função de complexidade seja:

[
T(n) = n \log_2(n) + \frac{3n}{2}
]

considerando uma função `Func()`.

**ATENÇÃO:** É permitido **somente** o uso de operadores aritméticos simples (adição, subtração, divisão e multiplicação) e **somente 2 laços**.

---

## Questão 03 (15%)

Aplique o **Teorema Mestre** na equação de recorrência:

[
T(n) = 9T(n/3) + n^2
]

Deixe explícito o seu raciocínio.

---

## Questão 04 (20%)

Encontre a ordem ( O ) de complexidade do código abaixo.

Deixe claro seu raciocínio, apresentando e desenvolvendo a função de complexidade.

**ATENÇÃO:** É obrigatório o uso da **expansão telescópica**.

```pseudo
Func(V, i, f)
    Se i < f
        m ← (f + i)/2
        Func(V, i, m)
        Func(V, m + 1, f)
        Para x ← i até m
            swp(V, x, x + 1)
        Fim Para
    Fim Se
Fim Func
```

---

## Questão 05 (20%)

Apresente e explique a função e a complexidade do código abaixo considerando o **pior e melhor caso**.

Além disso, apresente as condições necessárias para que cada uma ocorra, justificando sua resposta.

**ATENÇÃO:** Considere que o custo de execução de qualquer linha de comando seja igual a 1.

```pseudo
Func(V)
    f ← falso
    Enquanto f = falso
        f ← verdadeiro

        Para i ← 2 até V.n com passo +2
            Se V[i] > V[i + 1] então
                f ← falso
                swp(V, i, i + 1)
            Fim Se
        Fim Para

        Para i ← 1 até V.n com passo +2
            Se V[i] > V[i + 1] então
                f ← falso
                swp(V, i, i + 1)
            Fim Se
        Fim Para

    Fim Enquanto
Fim Func
```

---

