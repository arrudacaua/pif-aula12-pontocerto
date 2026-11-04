# Respostas da dupla — Atividade PontoCerto

## Dupla

| Papel | Nome completo | Usuário do GitHub |
|---|---|---|
| Integrante 1 (dono do fork) | Cauã Ferreira Arruda | arrudacaua |
| Integrante 2 (colaborador) | | |

## Explicação da solução

A função `calculaPontos` recebe uma regra como parâmetro e aplica essa regra ao valor informado. Assim, podemos reutilizar a mesma função com diferentes campanhas, sem precisar criar uma função para cada situação. As fábricas de campanhas permitem criar regras personalizadas, como multiplicar ou adicionar pontos. Isso evita repetição de código e facilita a criação de novas promoções.

## Desafio 2

Nas duas promoções de um dia, faz sentido utilizar lambdas porque são regras específicas e que não precisam ser reutilizadas em outras partes do programa. A lambda permite criar uma função anônima diretamente na chamada de `calculaPontos`, deixando o código mais simples e evitando criar funções nomeadas desnecessárias.

## Desafio 3

A expressão `campanhaMultiplicadora 5` devolve outra função, e não um número. Essa função recebe uma quantidade de pontos e multiplica por 5. Podemos confirmar isso no GHCi utilizando `:t campanhaMultiplicadora 5`, que apresenta o tipo `Int -> Int`. Isso significa que o resultado recebe um inteiro e devolve outro inteiro.

## Desafio 4

**a)** As duas ordens dão resultados diferentes porque a primeira campanha é aplicada antes da segunda. Na primeira ordem, multiplicamos 150 por 5, obtendo 750, e depois adicionamos 200, chegando a 950. Na segunda ordem, adicionamos 200 aos 150, obtendo 350, e depois multiplicamos por 5, chegando a 1750.

**b)** A ordem correta é primeiro aplicar a multiplicação e depois adicionar o bônus de aniversário. Assim, o bônus é acrescentado depois da multiplicação e não sofre o multiplicador.

## Desafio 5 — revisão de código

| Erro | Função | O que estava errado | Como o GHC avisou (resumo da mensagem) | Como corrigimos |
|---|---|---|---|---|
| 1 | aplicaRegraDuasVezes | O tipo de `regra` foi declarado como inteiro, mas ela deveria ser uma função. | Incompatibilidade entre o tipo `Int` esperado e o tipo de função `Int -> Int`. | Alteramos a assinatura para `(Int -> Int) -> Int -> Int`. |
| 2 | fimDeSemana | Foi utilizado `=>` em vez da seta correta para lambda. | Erro de sintaxe na expressão lambda. | Substituímos `=>` por `->`. |
| 3 | natal | A fábrica `campanhaBonus` não recebeu o valor do bônus. | Incompatibilidade de tipos: a função precisava retornar `Int`, mas recebeu uma função que ainda precisava de um argumento. | Alteramos para `natal = campanhaBonus 300`. |
| 4 | promocaoAtual | A função `pontosEmDobro` foi aplicada ao número 100 na definição, produzindo um inteiro em vez de uma função. | Incompatibilidade entre o tipo `Int -> Int` esperado e o tipo `Int` recebido. | Alteramos para `promocaoAtual = pontosEmDobro`. |

## Desafio 6 — Haskell × C

Uma diferença é que, em Haskell, podemos passar funções diretamente como parâmetros, utilizando o tipo `(Int -> Int)`. Em C, precisamos declarar explicitamente um ponteiro para função, utilizando a sintaxe `int (*regra)(int)`.

Outra diferença é que Haskell utiliza tipagem funcional e permite criar funções de forma mais direta com lambdas. Em C, precisamos declarar as funções separadamente e utilizar ponteiros para chamá-las indiretamente. Apesar das diferenças, as duas linguagens conseguem aplicar regras de pontuação de maneira reutilizável.

## Evidência de execução

Saída do `main` de `fidelidade.hs`:

```text
--- Desafio 1 ---
120
240
170
240
--- Desafio 2 ---
80
160
130
240
170
--- Desafio 3 ---
750
350
100
55
--- Desafio 4 ---
950
1750
280
```

Saída do `main` de `revisao.hs` (depois de corrigido):

```text
40
100
400
200
```

Saída de `pontocerto.c`:

```text
160
130
250
300
```
