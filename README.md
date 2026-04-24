# DataLakehouse Study

> Estudo prático de **Apache Spark** com **Delta Lake** e **Apache Iceberg** — Arquitetura de Dados | SATC

[![Python](https://img.shields.io/badge/python-3.11-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Poetry](https://img.shields.io/badge/gerenciador-poetry-60A5FA)](https://python-poetry.org/)
[![Apache Spark](https://img.shields.io/badge/spark-3.5.1-E25A1C?logo=apachespark&logoColor=white)](https://spark.apache.org/)

## Objetivo

Este repositório cria um ambiente local completo para estudar e testar:
- Apache Spark 3.5.1 com PySpark
- Delta Lake 3.2.0
- Apache Iceberg via Spark
- JupyterLab e notebooks interativos

## Estrutura do projeto

- `notebooks/delta_lake.ipynb` — demonstração Delta Lake com Spark
- `notebooks/iceberg.ipynb` — demonstração Apache Iceberg com Spark
- `docs/` — documentação do projeto e conceitos
- `pyproject.toml` — dependências e configuração do Poetry

## Pré-requisitos

1. Java 17 instalado e configurado em `JAVA_HOME`
   - Exemplo: `JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64`
2. Python 3.11 instalado
3. Poetry instalado
4. Conexão com internet para baixar dependências PyPI e pacotes Spark/Iceberg Maven

## Instalação do ambiente

```bash
git clone https://github.com/GabrielNM12/datalakehouse-study
cd datalakehouse-study
poetry config virtualenvs.in-project true
poetry install
```

> Se você usar o Visual Studio Code, abra a pasta `datalakehouse-study` e selecione o ambiente do Poetry em `.venv`.

## Executar o JupyterLab

```bash
poetry run jupyter lab
```

Em seguida, abra e execute as células dos notebooks:
- `notebooks/delta_lake.ipynb`
- `notebooks/iceberg.ipynb`

## Como usar no VS Code

1. Instale a extensão **Jupyter** do VS Code.
2. Abra `notebooks/delta_lake.ipynb` ou `notebooks/iceberg.ipynb`.
3. Selecione o kernel Python do Poetry (`.venv`).
4. Execute as células na ordem.

## Configuração do Spark para Delta Lake

O notebook `delta_lake.ipynb` usa a integração do pacote `delta-spark` com Spark.
A sessão Spark é configurada automaticamente com as extensões Delta e o catálogo Delta.

## Configuração do Spark para Apache Iceberg

O notebook `iceberg.ipynb` usa o catálogo Spark Iceberg com o pacote Maven:

- `org.apache.iceberg:iceberg-spark-runtime-3.5_2.12:1.3.0`

O código do notebook configura:

- `spark.sql.extensions`
- `spark.sql.catalog.local`
- `spark.sql.catalog.local.type`
- `spark.sql.catalog.local.warehouse`

## Notebooks de demonstração

- `notebooks/delta_lake.ipynb`: exemplo de escrita, leitura, atualização e time travel com Delta Lake.
- `notebooks/iceberg.ipynb`: exemplo de criação de tabela Iceberg, inserção, leitura e evolução de schema.

## Links úteis

- [Apache Spark](https://spark.apache.org/)
- [Delta Lake](https://delta.io/)
- [Apache Iceberg](https://iceberg.apache.org/)
- [Poetry](https://python-poetry.org/)

## Observações

- O código do Iceberg depende de download de pacotes Maven.
- Caso ocorra problema com `JAVA_HOME`, defina a variável para a instalação do Java 17.
