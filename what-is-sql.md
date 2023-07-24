## SQL - Structure Query Language
É uma linguagem padrão criada para operação em Bancos de Dados Relacionais.

A SQL foi criada no início dos anos 70 pela IBM. Após, foi padronizada pela ANSI e também pela ISO, que são duas entidades de regulação que colocaram ordem na SQL, por volta dos anos 80. Elas unificaram a linguagem em um padrão justamente para controlar os bancos de dados, e foi exatamente isso que deu origem ao que conhecemos hoje como SQL ANSI ou SQL Padrão.

O conceito por trás da linguagem é tão simples que não é necessário conhecer muito sobre o aspecto do hardware/software do banco de dados envolvido na operação. Basta executar as instruções SQL que as informações retornarão perfeitamente.

A SQL vêm sendo a linguagem padrão para comunicação com os bancos de dados há muitas décadas. Não há nada que mostre que os bancos de dados relacionais irão morrer, nem mesmo os bancos NoSQL.

Por conta disso, a SQL é importantíssima para quem trabalha com back-end e gosta da área de databases. O DBA (administrador de banco de dados) é uma das profissões mais interessantes e relevantes, já que gerencia dados de projetos e também de empresas.

## Principais SGBDs Relacionais
- MySQL
- SQL Server
- Oracle
- MariaDB
- PostgreSQL
- SQLite
- Sybase
- Informix
- Microsoft Access

## Utilidade
Com a SQL é possível inserir, excluír, alterar, selecionar, visualizar, ordenar, juntar, mesclar e intercalar os registros. Também é possível criar, alterar e remover as tabelas e alterar estruturas de dados nos campos das mesmas. Ainda dá pra inserir, remover e estabelecer relações entre as entidades, importar ou exportar dados entre as bases de dados. Criar chaves primárias, restrições e também chaves estrangeiras. Gerenciar os usuários com suas permissões de acesso. 

Vale ressaltar que nos sistemas um pouco mais avançados existem ainda: Triggers, Views, Stored Procedures e Functions.

## Código
A SQL é dividida em partes. O conceito por trás da linguagem é o de atuar em 3 frentes que chamamos de:

**LDD - Linguagem de Definição de Dados (CREATE, DROP e ALTER):**  
Utilizamos para manipular elementos do banco de dados como as tabelas, índices, views, procedures e usuários.

**LMD - Linguagem de Manipulação de Dados (SELECT, UPDATE, INSERT, DELETE):**  
Responsáveis pelos dados.

**LCD - Linguagem de Controle de Dados (GRANT, REVOKE):**  
Comandos para controle de permissões de acesso.

## Data Types
Um dos pontos muito importantes a citar sobre a SQL são os Data Types. De nada adiantaria a criação de uma linguagem padrão se os tipos de dados utilizados também não fossem padrão. Quando falamos sobre os Data Types temos que ter em mente os tipos de dados mais primitivos:

- Integer
- Char
- Long
- Float
- DateTime
- Binary

Cada SGBD tem independência pra criar seus próprios Data Types, mas os tipos padrão são na grande maioria respeitados. Um exemplo é o SQL Server, que tem um tipo de dado próprio para armazenar XML e até mesmo imagem.