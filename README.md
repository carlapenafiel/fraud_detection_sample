# Primeiros Passos com Detecção de Reformas

Bem-vindo ao projeto de Reformas e Cancelamentos. Este guia irá ajudá-lo a configurar o ambiente e executar o pipeline.

## Conteúdo

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Configuração do Ambiente](#configuração-do-ambiente)
  - [Pré-requisitos](#pré-requisitos)
  - [Instalação](#instalação)
- [Estrutura de Dados](#estrutura-de-dados)
- [Estrutura da Documentação e do Repositório](#estrutura-da-documentação-e-do-repositório)
  - [1. Modelo de Detecção de Outliers](#1-modelo-de-detecção-de-outliers)
  - [2. Modelo de Análise de Sazonalidade](#2-modelo-de-análise-de-sazonalidade)
  - [3. Modelo de Agrupamento de Reformas](#3-modelo-de-agrupamento-de-reformas)
  - [4. Modelo de Antecipação de Reformas](#4-modelo-de-antecipação-de-reformas)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Configuração do Ambiente

### Pré-requisitos

- Python 3.12 ou superior
- uv (ferramenta de empacotamento Python)

### Instalação

1. Clone o repositório:

   ```bash
   git clone <repository-url>
   cd ais-n4km-fraud-detection
   ```

2. Crie e ative um ambiente virtual usando uv:

   ```bash
   uv venv
   source .venv/bin/activate  # No Unix/macOS
   # .venv\Scripts\activate   # No Windows
   ```

3. Instale as dependências:

   ```bash
   uv pip install -e .
   ```

   Isso instalará automaticamente todas as dependências definidas no arquivo `pyproject.toml`.

## Estrutura de Dados

O pipeline espera dados na seguinte estrutura de diretórios:

```text
data/
├── raw/          # Arquivos de dados brutos
├── processed/    # Arquivos intermediários processados
└── results/      # Resultados dos modelos e avaliações
```

Se esses diretórios não existirem, crie-os:

```bash
mkdir -p data/raw data/processed data/results
```

Certifique-se de que seu arquivo de dados brutos esteja colocado no diretório `data/raw/` e configurado em `src/config.py`.

## Estrutura da Documentação e do Repositório

Este repositório está organizado para suportar quatro modelos principais para detecção e antecipação de reformas:

### 1. Modelo de Detecção de Outliers

Este modelo identifica anomalias nos dados de faturamento que podem indicar reformas. A implementação utiliza técnicas como Isolation Forest e análise estatística para detectar valores atípicos.

Principais componentes Outlier Consumo:

- notebooks_outliers_consumo/Model_Final_MM.ipynb
- notebooks_outliers_consumo/Experiments_Models_Outliers.ipynb
- notebooks_outliers_consumo/Features_test.ipynb
- notebooks_outliers_consumo/Grilla_Modelos.ipynb
- notebooks_outliers_consumo/MM_IF_Features_Model.ipynb
- notebooks_outliers_consumo/Modelo_Isolation_Forest.ipynb
- notebooks_outliers_consumo/Modelo_media_movil.ipynb

Principais componentes Outlier Valor:

- notebooks_outliers_valor/Modelo_No_Outliers_Valor_Facturado.ipynb

Documentação Outliers Consumo:

- [Outliers Consumo](docs/modelos/metodologia_outliers_consumo.md)
- [API de Outliers Consumo](docs/referencia_api/api_outliers_consumo.md)
- [Resultados](docs/resultados/resultados_outliers_consumo.md)

Documentação Outliers Valor Faturado:

- [Outliers Valor](docs/modelos/metodologia_outliers_valor.md)
- [API de Outliers Valor](docs/referencia_api/api_outliers_valor.md)
- [Resultados](docs/resultados/resultados_outliers_valor.md)

### 2. Modelo de Análise de Sazonalidade

Este modelo decompõe as séries temporais de faturamento para identificar padrões sazonais, tendências e componentes residuais que podem indicar anomalias.

Principais componentes:

- notebooks_sazonalidade/MM_Seasonality_FV.ipynb
- notebooks_sazonalidade/Model_Seasonality_Arquetipos.ipynb
- notebooks_sazonalidade/Model_Seasonality_Clusterizacion_Tests.ipynb

Documentação:

- [Sazonalidade](docs/modelos/modelo_sazonalidade.md)
- [API de Sazonalidade](docs/referencia_api/api_sazonalidade.md)
- [Resultados](docs/resultados/resultados_sazonalidade.md)

### 3. Modelo de Agrupamento de Reformas

Este modelo agrupa os clientes e suas reformas em padrões similares, permitindo identificar segmentos com comportamentos semelhantes.

Principais componentes:

- notebooks_clusterizacion/0_Testes_Clusterizacion.ipynb
- notebooks_clusterizacion/1_MM_Clusterizacion_Final.ipynb

Documentação:

- [Agrupamento](docs/modelos/metodologia_clusterizacao.md)
- [API de Agrupamento](docs/referencia_api/api_clusterizacao.md)
- [Resultados](docs/resultados/resultados_clusterizacao.md)

### 4. Modelo de Antecipação de Reformas

Este modelo utiliza aprendizado supervisionado para prever a probabilidade de reformas futuras, permitindo ações preventivas.

Principais componentes:

- notebooks_anticipacao_reformas/
  - 1_preproc.ipynb
  - 2_encode.ipynb
  - 3_run_train_and_tests.ipynb
  - 4_calibration.ipynb
  - 5_errors.ipynb
  - 6_optuna.ipynb
  - 7_shap.ipynb
- scripts/
  - run_preproc.py
  - run_encode.py
  - run_optuna.py
  - run_train.py

Documentação:

- [Anticipacao de reformas](docs/modelos/anticipacao_reformas.md)
- [API de Antecipação de Reformas](docs/referencia_api/api_anticipacao_de_reformas.md)
- [Resultados](docs/resultados/anticipacao_de_reformas.md)

A estrutura do código fonte (src/) contém módulos compartilhados entre todos os modelos, incluindo pré-processamento, codificação, métricas e utilidades.
