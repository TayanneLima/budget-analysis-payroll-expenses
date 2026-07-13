# Budget vs Forecast | Financial Planning & Analysis

<img width="1853" height="842" alt="image" src="https://github.com/user-attachments/assets/565f6c19-0445-4e93-8c41-47e484c8e3fd" />

Projeto de FP&A desenvolvido em Python para simular o acompanhamento orçamentário das despesas com pessoal de uma empresa, comparando Budget, Realizado e Forecast através de um dashboard executivo.

## Terminologia (importante para ler o relatório certo)

Este projeto compara três coisas que costumam ser confundidas:

| Termo | O que é |
|---|---|
| **Budget** | Plano anual, fechado no início do ano e fixo, não muda mês a mês |
| **Realizado** | O que de fato aconteceu, para os meses já fechados (Jan–Jul) |
| **Forecast** | A estimativa mais atual para os meses futuros (Ago–Dez), já incorporando informação nova (ex: headcount real) |

O relatório junta os dois em uma única visão anual — técnica de FP&A
chamada *Full Year Outlook*: `Budget vs. Realizado` para os meses fechados e
`Budget vs. Forecast` para os meses futuros. A planilha e o dashboard
marcam essa fronteira visualmente (cor azul = Realizado, dourado =
Forecast) para não deixar as duas coisas se misturarem no mesmo rótulo.

## Problema de negócio

Empresas precisam acompanhar continuamente se os gastos com pessoal estão aderentes ao orçamento aprovado. Para isso, é necessário comparar o Budget com o Realizado e o Forecast, identificar desvios relevantes e compreender seus principais direcionadores para apoiar a tomada de decisão.

Este projeto simula esse processo por meio de uma base de dados sintética, desenvolvida para reproduzir um cenário corporativo de acompanhamento orçamentário, permitindo a construção de uma análise de variância (Budget vs. Forecast) e de um dashboard executivo em Python.

## O que o projeto entrega

| Entrega | Descrição |
|---|---|
| `notebook/Analise_DRE.ipynb` | Notebook narrativo: cada gráfico vem acompanhado da leitura de negócio, não só do código |
| `outputs/dashboard.html` | Dashboard interativo (Plotly), um único arquivo HTML, sem servidor — abre em qualquer navegador |
| `outputs/DRE_Comparativa_Mensal.xlsx` | Planilha gerencial do Excel + aba de dados brutos |

## Principais insights encontrados

Junho teve um pico de rescisões acima do previsto. Esse evento elevou significativamente a despesa com rescisões, mas reduziu a folha salarial dos meses seguintes. Como consequência, Salários e Encargos Trabalhistas encerraram o ano com economia, compensando parte do impacto das rescisões e contribuindo para a economia consolidada de 0,30% frente ao orçamento.

*(Números completos e a leitura de cada gráfico estão no notebook.)*

## Funcionalidades

```

- Comparação entre Budget, Realizado e Forecast
- Cálculo automático de desvios financeiros
- Dashboard interativo desenvolvido em Plotly
- Exportação automática para Excel
- Geração de indicadores financeiros
- Identificação dos principais drivers de variação

```

## Desafios

Durante o desenvolvimento foi necessário:

- Definir premissas financeiras realistas.
- Simular regras de folha de pagamento.
- Construir dados sintéticos consistentes.
- Desenvolver indicadores próximos aos utilizados em FP&A.

## Stack

Python · pandas · numpy · openpyxl · matplotlib/seaborn · Plotly

## Sobre os dados

Todos os dados são **sintéticos**, gerados com seed fixa para
reprodutibilidade (`Premissas.seed`), mas a lógica de cálculo reproduz
regras reais de folha de pagamento (FGTS 8%, INSS patronal 20%, VR/VA
rateado por dias úteis, sazonalidade de férias e 13º salário, efeito de
admissões/demissões no headcount).
