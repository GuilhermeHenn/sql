## Primary Key (PK)
Uma Primary Key (chave primária, em português) é um conceito usado em bancos de dados relacionais para identificar de forma exclusiva cada registro em uma tabela. É um atributo (ou conjunto de atributos) que possui a característica de ser único e não nulo para cada linha na tabela.

A função principal da chave primária é garantir a integridade dos dados e fornecer um meio eficiente de acesso aos registros da tabela. Ela permite que os dados sejam organizados e relacionados entre as tabelas de um banco de dados. Além disso, a chave primária é usada como referência para estabelecer relacionamentos com outras tabelas, por meio de chaves estrangeiras.

Uma tabela em um banco de dados relacional pode ter apenas uma chave primária, e essa chave deve ser exclusiva para cada registro na tabela. Pode-se utilizar um único campo como chave primária, como um número de identificação único, ou combinar vários campos para formar uma chave composta.

As chaves primárias são importantes para a integridade e a consistência dos dados, pois impedem a duplicação de registros e fornecem uma maneira rápida de localizar informações específicas em uma tabela.

## Foreign Key (FK)
Uma Foreign Key (chave estrangeira, em português) é um conceito usado em bancos de dados relacionais para estabelecer um relacionamento entre duas tabelas. Ela é uma coluna (ou conjunto de colunas) em uma tabela que referencia a chave primária de outra tabela, criando assim uma ligação entre elas.

A chave estrangeira é utilizada para garantir a integridade referencial dos dados, ou seja, para manter a consistência entre as tabelas relacionadas. Ela estabelece uma restrição, indicando que os valores presentes na coluna da chave estrangeira devem corresponder aos valores existentes na coluna da chave primária da tabela referenciada.

Essa restrição impede a inserção de valores inválidos na tabela que contém a chave estrangeira, garantindo que os registros relacionados sempre apontem para registros válidos na tabela referenciada. Isso ajuda a evitar inconsistências e manter a integridade dos dados em um banco de dados relacional.

Uma chave estrangeira pode ser definida em uma tabela usando a declaração de chave estrangeira (FOREIGN KEY) durante a criação da tabela ou por meio de uma alteração posterior na estrutura da tabela. A chave estrangeira também pode ser configurada para realizar ações automáticas em cascata, como excluir registros relacionados quando o registro correspondente na tabela referenciada é excluído (ON DELETE CASCADE) ou atualizar valores automaticamente quando a chave primária é alterada (ON UPDATE CASCADE).

Em resumo, a chave estrangeira é utilizada para estabelecer relações entre tabelas em um banco de dados relacional, mantendo a integridade referencial dos dados e permitindo consultas e manipulações consistentes entre as tabelas relacionadas.