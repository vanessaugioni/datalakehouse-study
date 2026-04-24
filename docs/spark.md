# Apache Spark (PySpark)

Apache Spark é o motor de processamento em memória usado para trabalhar com grandes volumes de dados.

## Versão usada

- Apache Spark 3.5.1
- Python 3.11

## Como rodar localmente

O ambiente utiliza o Spark local com `master("local[*]")` para desenvolvimento e aprendizado.

## Integração com Delta e Iceberg

- Delta Lake: usa a extensão `io.delta.sql.DeltaSparkSessionExtension` e o catálogo `DeltaCatalog`.
- Apache Iceberg: usa o catálogo `org.apache.iceberg.spark.SparkCatalog` e o pacote Spark Iceberg runtime.

## Notebooks

- `notebooks/delta_lake.ipynb`
- `notebooks/iceberg.ipynb`
