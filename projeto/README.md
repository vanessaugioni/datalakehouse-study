# DataLakehouse Study

> Estudo prático de **Apache Spark** com **Delta Lake** e **Apache Iceberg** — Arquitetura de Dados | SATC

[![Python](https://img.shields.io/badge/python-3.11-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Poetry](https://img.shields.io/badge/gerenciador-poetry-60A5FA)](https://python-poetry.org/)
[![Apache Spark](https://img.shields.io/badge/spark-3.5.1-E25A1C?logo=apachespark&logoColor=white)](https://spark.apache.org/)

## Participantes

| Nome | GitHub |
|---|---|
| — | — |
| — | — |
| — | — |

## Documentação

📖 https://GabrielNM12.github.io/datalakehouse-study

## Como rodar

### Pré-requisitos

- Java 17 → [adoptium.net](https://adoptium.net/temurin/releases/?version=17)
- Python 3.11 → [python.org](https://www.python.org/downloads/)
- Poetry → [python-poetry.org](https://python-poetry.org/docs/#installation)

### Instalação

```bash
git clone https://github.com/GabrielNM12/datalakehouse-study
cd datalakehouse-study
poetry config virtualenvs.in-project true
poetry install
```

### Executar notebooks

```bash
poetry run jupyter lab
```

Abra e execute célula a célula:
- `notebooks/delta_lake.ipynb`
- `notebooks/iceberg.ipynb`
