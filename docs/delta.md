# Delta Lake

Delta Lake é uma camada de armazenamento transacional para Apache Spark que adiciona suporte a:

- ACID transactions
- Time travel
- Schema enforcement e schema evolution
- Compactação e otimização de tabelas

## Configuração no notebook

O notebook `notebooks/delta_lake.ipynb` configura o Spark com o pacote `delta-spark` e grava tabelas no formato Delta.

## O que aprender neste notebook

- Escrever um DataFrame como tabela Delta
- Ler dados Delta
- Atualizar registros com `DeltaTable`
- Consultar versões antigas usando `versionAsOf`
