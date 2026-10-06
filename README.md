# Desafio DIO - Star Schema com DAX

Este repositório apresenta a resolução do desafio proposto pela DIO, utilizando a base **Financial Sample** do Power BI para a criação de um modelo baseado em **Star Schema**.

Como parte do desafio, também foi criada uma tabela de calendário utilizando **DAX**, com o objetivo de organizar e facilitar a análise das informações relacionadas às datas das vendas.

## Tabela D_Calendário

Para criar a tabela de calendário, foi utilizada a função `CALENDAR()` em conjunto com `MIN()` e `MAX()`:

```DAX
D_Calendário =
CALENDAR(
    MIN(F_Vendas[Date]),
    MAX(F_Vendas[Date])
)
```

A função `MIN()` identifica a data mais antiga presente na tabela `F_Vendas`, enquanto `MAX()` identifica a data mais recente.

A função `CALENDAR()` utiliza essas duas datas para criar uma lista contendo todos os dias existentes entre a primeira e a última data de venda.

## Coluna Ano

Após a criação da tabela de calendário, foi criada uma coluna para identificar o ano correspondente a cada data:

```DAX
Ano = YEAR('D_Calendário'[Date])
```

A função `YEAR()` extrai o ano presente na coluna `Date`, permitindo utilizar o ano como informação de análise.

## Coluna Mês

Também foi criada uma coluna para identificar o mês de cada data:

```DAX
Mês = FORMAT('D_Calendário'[Date], "MMMM")
```

A função `FORMAT()` permite definir como a informação será apresentada. Nesse caso, o formato `"MMMM"` retorna o nome completo do mês correspondente à data.

## Modelo

O modelo foi organizado seguindo o conceito de **Star Schema**, utilizando a tabela `F_Vendas` como tabela fato e as demais tabelas como dimensões.

A tabela `D_Calendário` funciona como uma dimensão de datas, permitindo realizar análises das vendas de acordo com diferentes períodos.
