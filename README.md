# engenhariaCognitivo
Para a instalação do programa, é necessário ter os pacotes instalados:
  - pandas
  - sqlalchemy
  - pyodbc

Para Rodar o programa é necessário passar alguns argumentos na execução:
python engenharia.py 'pathToFiles' 'serverName' 'databaseName' 'driverName' 'schemaName'

  - pathToFiles >> caminho onde estão os arquivos base
  - serverName >> servidor destino SQL Server
  - databaseName >> banco onde ficarão inseridos os dados
  - driverName >> driver de conexão com o SQL Server. Eg. 'ODBC Driver 13 for SQL Server'
  - schemaName >> schema a ser utilizado
  
A autenticação no servidor será feita por Windows Autorization do usuário a ser utilizado no momento da execução.

O processo não mantém histórico de execução e sempre recria as tabelas a cada execução

---------------------------------------------------------------------------------------------------------------------------

Para a criação do modelo de dados, temos a leitura dos três arquivos (bill_of_materials.csv, comp_boss.csv, price_quote.csv). A partir destes arquivos, montou-se 3 tabelas Fato e 2 Dimensionais. A criação da fatoTubeAssemblyComponent foi devido à facilidade de trabalhar com os dados em forma de linhas e não colunas. A fatoPriceQuoteBracket e fatoPriceQuoteNBracket possibilita a separação dos tipos de cobrança e melhor avaliação em dashboards. O modelo com duas dimensões e 3 fatos foi criado para otimizar o uso de recursos e velocidade nas consultas.

Dimensionais:
  * dimTubeAssembly
  tube_assembly_id (string)
  
  * dimComponent
  component_id (string),
  component_type_id (string),
  type (string),
  connection_type_id (string),
  outside_shape (string),
  base_type (string),
  height_over_tube (float),
  bolt_pattern_long (float),
  bolt_pattern_wide (float),
  groove (string),
  base_diameter (float),
  shoulder_diameter (float),
  unique_feature (string),
  orientation (string),
  weight (float)

Fatos:
  * fatoTubeAssemblyComponent
  tube_assembly_id (string),
  component_id (string),
  component_index (int),
  quantity (int)
  
  * fatoPriceQuoteBracket
  tube_assembly_id (string),
  supplier (string),
  quote_date (date),
  quantity (int),
  cost (float)
  
  * fatoPriceQuoteNBracket
  tube_assembly_id (string),
  supplier (string),
  quote_date (date),
  annual_usage (int),
  min_order_quantity (int),
  quantity (int),
  cost (float)
  
  
