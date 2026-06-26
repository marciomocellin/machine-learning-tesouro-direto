# MVP — Previsão de Taxas do Tesouro Direto

Trabalho final da disciplina **Machine Learning & Analytics** da Especialização em Ciência de Dados e Big Data — PUC-Rio.

**Autor:** Marcio Goulart Mocellin  
**Matrícula:** 4052026000399  
**Data:** Julho de 2026

---

## Descrição

Este projeto desenvolve um MVP de Machine Learning para **prever a taxa de venda da manhã do Tesouro Prefixado** para o dia seguinte (horizonte de 1 dia). O problema é tratado como **regressão supervisionada sobre séries temporais**, utilizando a abordagem de janela deslizante (*sliding window*) para transformar a série em features de lag.

O notebook é completamente reproduzível no Google Colab — os dados são carregados diretamente via URL pública, sem necessidade de upload, login ou configuração local.

---

## Dataset

- **Fonte:** Tesouro Nacional — Dados Abertos ([Tesouro Transparente](https://www.tesourotransparente.gov.br/ckan/dataset/df56aa42-484a-4a59-8184-7676580c81e3))
- **Arquivo:** [`precotaxatesourodireto.csv`](https://www.tesourotransparente.gov.br/ckan/dataset/df56aa42-484a-4a59-8184-7676580c81e3/resource/796d2059-14e9-44e3-80c9-2d9e30b405c1/download/precotaxatesourodireto.csv)
- **Metadados:** [taxa.pdf](https://www.tesourotransparente.gov.br/ckan/dataset/df56aa42-484a-4a59-8184-7676580c81e3/resource/1a8eb2e3-4902-4a38-a1eb-6410f23d90de/download/taxa.pdf)
- **Cobertura:** Preços e taxas diários de títulos do Tesouro Direto desde 2002
- **Variável-alvo:** `Taxa Venda Manha` (% a.a.) do Tesouro Prefixado

---

## Estrutura do Notebook

| Seção | Conteúdo |
|---|---|
| 1. Apresentação do Problema | Descrição, objetivo, tipo de tarefa e premissas |
| 2. Configuração do Ambiente | Importações e dependências |
| 3. Carregamento dos Dados | Leitura via URL pública |
| 4. Apresentação dos Dados | Primeiras linhas, tipos, descrição dos atributos |
| 5. Análise Exploratória | Séries temporais, distribuição, ACF/PACF |
| 6. Preparação dos Dados | Tratamento de ausentes, engenharia de features |
| 7. Divisão Temporal | Corte 80% treino / 20% teste |
| 8. Modelagem | Baselines + 5 modelos candidatos |
| 9. Otimização | GridSearchCV com TimeSeriesSplit |
| 10. Avaliação | Métricas, gráficos, análise de overfitting |
| 11. Conclusão | Resumo, limitações e próximos passos |
| 12. Checklist do MVP | Verificação de todos os critérios da disciplina |

---

## Modelos Avaliados

| Categoria | Modelo |
|---|---|
| Baseline | Persistência Ingênua (lag_1) |
| Baseline | Média Móvel 21 dias |
| Linear | Regressão Linear |
| Linear | Ridge Regression |
| Ensemble | Random Forest |
| Ensemble | Gradient Boosting |
| Ensemble | Extra Trees |
| Otimizado | Random Forest (GridSearchCV + TimeSeriesSplit) |

---

## Engenharia de Features

| Feature | Descrição |
|---|---|
| `lag_1` a `lag_21` | Valores defasados (1, 2, 3, 5, 10, 21 dias) |
| `roll_mean_5`, `roll_mean_21` | Média móvel de 5 e 21 dias |
| `roll_std_5`, `roll_std_21` | Desvio padrão móvel de 5 e 21 dias |
| `diff_1`, `diff_5` | Variação em 1 e 5 dias (momentum) |
| `month`, `quarter`, `day_of_week` | Features de calendário |
| `time_idx` | Índice de tendência linear |

Todas as features de lag e rolling usam `.shift(1)` para **evitar vazamento de dados**.

---

## Métricas de Avaliação

- **MAE** — Erro Médio Absoluto (escala original, em p.p.)
- **RMSE** — Raiz do Erro Quadrático Médio (penaliza erros grandes)
- **MAPE** — Erro Percentual Absoluto Médio (comparação relativa)
- **R²** — Coeficiente de Determinação

---

## Principais Resultados

O **Random Forest Otimizado** (via GridSearchCV com TimeSeriesSplit) obteve o melhor desempenho no conjunto de teste, superando todos os baselines e os demais modelos. A alta autocorrelação da série (>0,99 para lag=1) explica por que o baseline de persistência já é competitivo, e por que os ganhos adicionais dos modelos supervisionados são incrementais.

---

## Limitações

1. Abordagem **univariada** — sem variáveis macroeconômicas externas (IPCA, câmbio, boletim Focus)
2. Horizonte fixo de **1 dia à frente**
3. Análise restrita a **um único título** (Tesouro Prefixado)
4. Avaliação **estática** — sem re-treino periódico

---

## Como Executar

Abra o notebook [`MVP_Machine_Learning_Tesouro_Direto.ipynb`](MVP_Machine_Learning_Tesouro_Direto.ipynb) no Google Colab e execute todas as células em sequência. Nenhuma configuração adicional é necessária.

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/marciomocellin/machine-learning-tesouro-direto/blob/main/MVP_Machine_Learning_Tesouro_Direto.ipynb)

---

## Dependências

```
pandas
numpy
matplotlib
seaborn
scikit-learn
statsmodels
```

Todas as bibliotecas estão disponíveis no ambiente padrão do Google Colab.
