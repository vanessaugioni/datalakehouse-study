# Delta Lake

## O que é

**Delta Lake** é uma camada de armazenamento open-source que adiciona confiabilidade ao Data Lake. Ele traz transações **ACID**, controle de versão, schema enforcement e auditoria para arquivos Parquet armazenados em sistemas de arquivos locais ou na nuvem (S3, ADLS, GCS).

---

## Principais Recursos

| Recurso | Descrição |
|---|---|
| **Transações ACID** | Garante consistência mesmo em falhas ou escritas concorrentes |
| **Time Travel** | Consulta versões anteriores dos dados pelo número de versão ou timestamp |
| **Schema Enforcement** | Impede a escrita de dados com schema incompatível |
| **Schema Evolution** | Permite adicionar ou modificar colunas de forma controlada |
| **Delta Log** | Arquivo de transações JSON que registra cada operação na tabela |

---

## Como funciona

Cada tabela Delta é um diretório com arquivos Parquet + uma pasta `_delta_log/`. O Delta Log registra cada operação (add, remove, update) em arquivos JSON sequenciais. Isso é o que permite o time travel e as garantias ACID.

```
delta_table/
├── part-00000.parquet
├── part-00001.parquet
└── _delta_log/
    ├── 00000000000000000000.json   ← versão 0 (INSERT inicial)
    └── 00000000000000000001.json   ← versão 1 (UPDATE)
```

---

## Implementação no Projeto

### 1. Configurar a SparkSession

```python
import os
from pyspark.sql import SparkSession
from delta import configure_spark_with_delta_pip

builder = (
    SparkSession.builder
    .appName("DeltaLakeStudy")
    .master("local[*]")
    .config("spark.sql.extensions", "io.delta.sql.DeltaSparkSessionExtension")
    .config("spark.sql.catalog.spark_catalog", "org.apache.spark.sql.delta.catalog.DeltaCatalog")
)

spark = configure_spark_with_delta_pip(builder).getOrCreate()

delta_path = os.path.abspath("tmp/delta_table")
```

### 2. INSERT — Criar e popular a tabela

```python
data = [(1, "Alice", 1200), (2, "Bob", 1500), (3, "Carol", 1600)]
df = spark.createDataFrame(data, ["id", "name", "salary"])

df.write.format("delta").mode("overwrite").save(delta_path)
```

Registrar como tabela SQL:

```python
spark.sql("DROP TABLE IF EXISTS delta_demo")
spark.sql(f"CREATE TABLE delta_demo USING DELTA LOCATION '{delta_path}'")
spark.sql("SELECT * FROM delta_demo").show()
```

Resultado:

```
+---+-----+------+
| id| name|salary|
+---+-----+------+
|  1|Alice|  1200|
|  2|  Bob|  1500|
|  3|Carol|  1600|
+---+-----+------+
```

### 3. UPDATE — Atualizar um registro

```python
from delta.tables import DeltaTable

delta_table = DeltaTable.forPath(spark, delta_path)
delta_table.update("id = 1", {"salary": "salary + 400"})

spark.read.format("delta").load(delta_path).show()
```

Resultado após o UPDATE (salário de Alice passou de 1200 para 7000 após múltiplas execuções):

```
+---+-----+------+
| id| name|salary|
+---+-----+------+
|  1|Alice|  7000|
|  3|Carol|  1600|
|  2|  Bob|  1500|
+---+-----+------+
```

### 4. Time Travel — Consultar versão anterior

```python
print("Versão 0 - antes da atualização")
spark.read.format("delta").option("versionAsOf", 0).load(delta_path).show()
```

Resultado — dados originais antes de qualquer UPDATE:

```
+---+-----+------+
| id| name|salary|
+---+-----+------+
|  1|Alice|  1200|
|  2|  Bob|  1500|
|  3|Carol|  1600|
+---+-----+------+
```

### 5. DELETE — Remover um registro

```python
delta_table.delete("id = 2")
spark.read.format("delta").load(delta_path).show()
```

---

## Delta Log — Rastreando o histórico

```python
from delta.tables import DeltaTable

delta_table = DeltaTable.forPath(spark, delta_path)
delta_table.history().show(truncate=False)
```

Cada operação (WRITE, UPDATE, DELETE) gera uma nova entrada no log com timestamp, versão e tipo de operação.

---

## Referências

- [Documentação oficial Delta Lake](https://docs.delta.io/)
- [delta-spark no PyPI](https://pypi.org/project/delta-spark/)
- [Canal DataWay BR](https://www.youtube.com/@DataWayBR)
- [jlsilva01/spark-delta](https://github.com/jlsilva01/spark-delta)
