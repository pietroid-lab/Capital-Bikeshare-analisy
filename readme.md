🚀 Como Executar o Projeto
1. 📦 Pré-requisitos

Instale:

Python 3.9+

Jupyter Notebook ou JupyterLab

Redis (opcional)
# P2 — Ciências de Dados

## 🚀 Objetivo

## 📊 Tráfego de Bicicletas Compartilhadas – Capital Bikeshare (Bike Sharing Dataset)
Este repositório contém um notebook para análise e modelagem de séries temporais (ARIMA) sobre o dataset diário `day.csv`, além de exemplos de estruturas probabilísticas (HyperLogLog, Count-Min Sketch) implementadas com Redis/RedisBloom ou simuladas com `fakeredis`.

## 📦 Pré-requisitos
- Python 3.9+
- Jupyter Notebook ou JupyterLab
- Redis (opcional para execução real das estruturas probabilísticas)
- Docker (opcional — recomendado para Redis + RedisBloom)

## 📥 Instalar dependências
Execute (recomendado em um ambiente virtual):

```bash
pip install pandas numpy matplotlib statsmodels scikit-learn redis redisbloom fakeredis jupyter nbformat
```

## 📂 Preparar o dataset
Coloque o arquivo `day.csv` em `data/` (ex.: `data/day.csv`).

Se o arquivo estiver em outro local, ajuste a variável `csv_path` dentro do notebook `notebooks/analysis.ipynb`.

## ▶️ Executar o notebook
No terminal execute um dos comandos:

```bash
jupyter notebook
# ou
jupyter lab
```

Abra `notebooks/analysis.ipynb` e execute as células na ordem.

## 📊 O que o notebook faz (resumo)
- Análise Exploratória (estatísticas descritivas, plots da série temporal)
- Cálculo de médias móveis (7, 30 e 90 dias)
- Decomposição sazonal (tendência, sazonalidade, ruído)
- Plots de ACF e PACF para suporte à seleção de parâmetros ARIMA (p, d, q)
- Grid search por AIC, treinamento do melhor modelo ARIMA e geração de previsões com intervalos de confiança
- Cálculo de métricas: RMSE, MAE, MAPE
- Avaliação de horizontes de previsão: 7, 14, 30 e 60 dias

## 🔢 Estruturas probabilísticas (Redis / RedisBloom)
O notebook inclui implementações para:

- **HyperLogLog** — estimativa de cardinalidade (ex.: número de categorias distintas de `weathersit` em janelas de 30 dias)
- **Count-Min Sketch** — estimativa aproximada de frequências para buckets da coluna `cnt`

As implementações suportam:
- Execução real usando Redis + RedisBloom
- Execução simulada usando `fakeredis` (sem necessidade de Redis instalado)

## 🧰 Usando Redis (opções)
Opção A — Rodar Redis + RedisBloom via Docker (exemplo recomendado):

```bash
docker run -p 6379:6379 redislabs/rebloom:latest
```

O notebook irá conectar em `localhost:6379` por padrão.

Opção B — Usar `fakeredis` (modo simulado)

O notebook detecta a ausência de um servidor Redis e instancia `fakeredis.FakeStrictRedis()` automaticamente.

## 📤 Artefatos gerados (após execução)
Os arquivos a seguir são gravados em `outputs/`:

- `cnt_series.csv`
- `arima_aic_rankings.csv`
- `hll_estimates.csv`
- `cms_comparison.csv`

## 📝 Observações importantes
- Divisão de treino/teste: 80% / 20%
- Dataset principal: `day.csv`
- Coluna de data: `dteday`
- Fuso horário aplicado: `America/Sao_Paulo`
- Melhores horizontes são escolhidos automaticamente com base nas métricas de erro
- Redis é opcional — usar Docker+RedisBloom permite testar as estruturas probabilísticas em produção
