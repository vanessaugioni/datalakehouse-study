# Apache Iceberg

Apache Iceberg é um formato de tabela aberto para grandes dados, projetado para oferecer:

- gerenciamento de metadados eficiente
- suporte a operações transacionais
- evoluções de schema sem reescrever todos os dados
- compatibilidade com catálogos Hadoop, Hive, AWS Glue e outros

## Configuração no notebook

O notebook `notebooks/iceberg.ipynb` configura o Spark para usar o catálogo Iceberg local com Hadoop.

## O que aprender neste notebook

- Criar uma tabela Iceberg
- Inserir dados usando Spark
- Ler dados de uma tabela Iceberg
- Alterar schema com `ALTER TABLE`
