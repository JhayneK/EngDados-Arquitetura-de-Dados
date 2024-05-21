# EngDados-Arquitetura-de-Dados
EngDados-Arquitetura-de-Dados

# Configuração do Ambiente PySpark e Jupyter Labs com Delta Lake e Apache Iceberg

Este repositório contém instruções para configurar um ambiente de desenvolvimento PySpark e Jupyter Labs, incluindo a implementação do Delta Lake e Apache Iceberg usando pip.

## Pré-requisitos

Antes de começar, verifique se você possui o seguinte instalado em seu sistema:

- Python 3.10.6
- pip (gerenciador de pacotes Python) 22.2.1
- Java JDK (para o ambiente Spark) 17.0.11
- Spark (pode ser instalado via pip ou baixado do site oficial)

## Instalação

1. Clone este repositório em sua máquina local:

    ```bash
    https://github.com/JhayneK/EngDados-Arquitetura-de-Dados.git
    ```

2. Navegue até o diretório do projeto:

    ```bash
    cd seu-repositorio
    ```

3. Instale os pacotes necessários usando pip:

    ```bash
    pip install pyspark jupyterlab delta-lake apache-iceberg
    ```

## Configuração do Ambiente

1. Inicie o Jupyter Labs:

    ```bash
    jupyter lab
    ```

2. Crie um novo notebook Python no Jupyter Labs.

3. Importe o PySpark e inicie a sessão Spark:

    ```python
    from pyspark.sql import SparkSession

    spark = SparkSession.builder \
        .appName("Exemplo Delta Lake e Apache Iceberg") \
        .getOrCreate()
    ```

## Uso do Delta Lake e Apache Iceberg

Agora você pode usar o Delta Lake e o Apache Iceberg em seu notebook PySpark. Aqui está um exemplo básico de como criar uma tabela Delta usando o Apache Iceberg:

```python
# Importe o módulo Delta Lake
from delta.tables import *

# Caminho para armazenar a tabela Delta
delta_path = "caminho/para/sua/tabela/delta"

# Crie um DataFrame de exemplo
data = [("Alice", 34), ("Bob", 45), ("Charlie", 27)]
df = spark.createDataFrame(data, ["Nome", "Idade"])

# Salve o DataFrame como uma tabela Delta
df.write.format("delta").save(delta_path)

# Leia a tabela Delta usando Apache Iceberg
delta_table = DeltaTable.forPath(spark, delta_path)

# Exiba o histórico de versões da tabela
delta_table.history().show()

