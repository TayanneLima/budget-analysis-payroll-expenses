# DRE de Custos de Pessoal — Análise de Variância (Budget vs. Forecast)

Projeto de portfólio de FP&A (Financial Planning & Analysis): simula o
acompanhamento mensal do orçamento de folha de pagamento de uma empresa
fictícia de **1.134 funcionários**, comparando o **Orçado (Budget)** com o
**Realizado/Projetado (Forecast)** ao longo de 12 meses, e identifica onde
estão os principais desvios e por quê.

**[Ver o dashboard interativo →](outputs/dashboard.html)** · [Ver o notebook com a análise completa →](notebook/Analise_DRE.ipynb) · [Baixar a planilha Excel →](outputs/DRE_Comparativa_Mensal.xlsx)

## Terminologia (importante para ler o relatório certo)

Este projeto compara três coisas que costumam ser confundidas:

| Termo | O que é |
|---|---|
| **Budget** | Plano anual, fechado no início do ano e **fixo** — não muda mês a mês |
| **Realizado** | O que de fato aconteceu, para os meses já fechados (Jan–Jul) |
| **Forecast** | A estimativa mais atual para os meses futuros (Ago–Dez), já incorporando informação nova (ex: headcount real) |

O relatório junta os dois em uma única visão anual — técnica de FP&A
chamada *Full Year Outlook*: `Budget vs. Realizado` para os meses fechados e
`Budget vs. Forecast` para os meses futuros. A planilha e o dashboard
marcam essa fronteira visualmente (cor azul = Realizado, dourado =
Forecast) para não deixar as duas coisas se misturarem no mesmo rótulo.

## Problema de negócio

Toda empresa com folha de pagamento relevante precisa responder, mês a mês,
a uma pergunta simples que raramente tem resposta simples: **"gastamos mais
ou menos do que planejamos, e por quê?"**. Este projeto simula esse
processo: gera dados sintéticos (mas com regras reais de folha brasileira —
FGTS, INSS, VR/VA proporcional, sazonalidade de férias e 13º) e constrói
uma análise de variância completa em cima deles.

## O que o projeto entrega

| Entregável | Descrição |
|---|---|
| `notebook/Analise_DRE.ipynb` | Notebook narrativo: cada gráfico vem acompanhado da leitura de negócio, não só do código |
| `outputs/dashboard.html` | Dashboard interativo (Plotly), um único arquivo HTML, sem servidor — abre em qualquer navegador |
| `outputs/DRE_Comparativa_Mensal.xlsx` | Planilha gerencial com fórmulas nativas do Excel (recalcula sozinha) + aba de dados brutos |
| `src/` | Código-fonte modular (geração de dados, análise, exportação, visualização) |

## Principais insights encontrados

- Desvio anual consolidado de **+0,30%** sobre o orçado — processo
  orçamentário bem calibrado no agregado.
- **Salários e ordenados** ficou ~R$ 274 mil acima do orçado (efeito do
  crescimento real de headcount), enquanto **Rescisões** ficou ~R$ 238 mil
  abaixo — dois desvios grandes que quase se cancelam no total, mas contam
  histórias de negócio opostas.
- **Encargos Trabalhistas** é o grupo proporcionalmente mais desviado
  (+0,45%), o que é esperado: FGTS/INSS são calculados sobre a folha, então
  herdam automaticamente o desvio de Salários.

*(Números completos e a leitura de cada gráfico estão no notebook.)*

## Estrutura do projeto

```
dre_folha_pagamento/
├── README.md
├── requirements.txt
├── main.py                      # gera todos os entregáveis de uma vez
├── src/
│   ├── data_generator.py        # geração dos dados sintéticos (regras de folha)
│   ├── analysis.py               # cálculos de variância, KPIs, tendências
│   ├── excel_export.py          # exportação para Excel com fórmulas nativas
│   ├── dashboard.py              # geração do dashboard HTML/Plotly
│   └── visualizations.py         # gráficos estáticos usados no notebook
├── notebook/
│   └── Analise_DRE.ipynb         # análise narrativa, ponta a ponta
└── outputs/
    ├── DRE_Comparativa_Mensal.xlsx
    └── dashboard.html
```

## Como rodar

```bash
pip install -r requirements.txt
python main.py
```

Isso regenera `outputs/DRE_Comparativa_Mensal.xlsx` e `outputs/dashboard.html`
a partir do zero. Para a versão narrativa com a interpretação de cada
gráfico, abra `notebook/Analise_DRE.ipynb`.

## Stack

Python · pandas · numpy · openpyxl · matplotlib/seaborn · Plotly

## Sobre os dados

Todos os dados são **sintéticos**, gerados com seed fixa para
reprodutibilidade (`Premissas.seed`), mas a lógica de cálculo reproduz
regras reais de folha de pagamento (FGTS 8%, INSS patronal 20%, VR/VA
rateado por dias úteis, sazonalidade de férias e 13º salário, efeito de
admissões/demissões no headcount).
