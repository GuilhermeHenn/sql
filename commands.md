## Estrutura para consultas
```sql
-- seleção do database
USE base;

-- seleção dos atributos (colunas)
SELECT 
  atributo1,
  atributo2,
  atributo3
-- seleção da entidade (tabela)
FROM table1
-- filtro
WHERE atributo2 >= 10
-- ordenação
ORDER BY atributo3;
```

```sql
USE sakila;

SELECT 
  venda_id,
  cliente, 
  valor,
  -- coluna personalizada de nome "10% de desconto"
  valor - (valor * 0.10) AS '10% de desconto'
FROM venda
WHERE venda_id < 300;
```

```sql
USE sakila;

-- seleção de todos os atributos
SELECT * 
FROM payment
WHERE amount != 2
-- ordenação decrescente/crescente
ORDER BY amount DESC;
-- ORDER BY amount ASC;
```

## LIMIT - Limite de linhas
```sql
USE sakila;

SELECT *
FROM actor
-- limita a listagem em 10 linhas (rows)
LIMIT 10;
```

```sql
USE sakila;

SELECT * 
FROM actor
-- lista 10 linhas a partir da 5ª linha
LIMIT 5, 10;
```

## Filtros e Operadores
```sql
USE sakila;

SELECT * 
FROM adress
-- filtro por texto
WHERE district = 'Texas';
```

```sql
USE sakila;

SELECT *
FROM payment
-- operador "e"
WHERE staff_id = 1 AND amount = 0.99 AND customer_id < 10;
```

```sql
USE sakila;

SELECT * 
FROM payment
-- operador "ou"
WHERE staff_id = 1 OR amount = 0.99;
```

```sql
USE sakila;

SELECT * 
FROM payment
-- operador de "negação"
WHERE NOT staff_id = 1 AND amount = 0.99;
```

```sql
USE sakila;

SELECT *
FROM address
-- filtro por mais de um valor (semelhante ao OR)
-- WHERE district = 'Alberta' OR district = 'Texas' OR district = 'California'
WHERE district IN ('Alberta', 'Texas', 'California')
ORDER BY address_id;
```

```sql
USE sakila;

SELECT * 
FROM payment
-- amount entre 1.99 e 3.99
-- WHERE amount >= 1.99 AND amount <= 3.99
WHERE amount BETWEEN 1.99 AND 3.99;
```

```sql
USE sakila;

SELECT * 
FROM actor
-- finaliza com "ay"
WHERE first_name LIKE '%ay';
-- começa com "ca"
WHERE first_name LIKE 'ca%';
-- contém "li" em meio a palavra
WHERE first_name LIKE '%li%';
-- "_" representa (corresponde a) qualquer um único caractere
WHERE first_name LIKE '_li_';
```

```sql
USE sakila;

SELECT *
FROM address
-- filtro por campos vazios (sem valor)
WHERE address2 IS NULL;
```

```sql
USE sakila;

SELECT *
FROM actor
-- valores que começam com "a", "d" ou "r"
WHERE first_name REGEXP '^a|^d|^r'
ORDER BY first_name;
```

```sql
USE sakila;

SELECT * 
FROM actor
-- valores que contém "a"
WHERE first_name REGEXP 'a';
```

```sql
USE sakila;

SELECT *
FROM actor
-- valores que contém "ga", "ea" ou "ra"
WHERE first_name REGEXP '[ger]a'
ORDER BY first_name;
```

```sql
USE sakila;

SELECT *
FROM actor
-- valores que começam com "ga", "ca" ou "ra"
WHERE first_name REGEXP '^[grc]a'
ORDER BY first_name;
```

## JOIN
O "JOIN" é uma cláusula essencial da linguagem SQL (Structured Query Language) usada para combinar dados de duas ou mais tabelas em uma única consulta. Essa cláusula permite que você recupere informações relacionadas de várias tabelas em uma única saída, com base em colunas que têm valores em comum nas tabelas envolvidas.
```sql
USE sakila;

SELECT 
  customer.customer_id,
  customer.first_name,
  customer.last_name,
  payment.rental_id,
  payment.amount
FROM customer
-- junção dos dados da tabela 'customer' com os dados da tabela 'payment'
-- vínculo do 'customer_id' da tabela 'customer' com o 'customer_id' da tabela 'payment'
JOIN payment ON customer.customer_id = payment.customer_id;
```

```sql
USE sakila;

SELECT 
  cus.customer_id,
  cus.first_name,
  cus.last_name,
  pay.rental_id,
  pay.amount
-- criando alias "cus"
FROM customer cus
-- criando alias "pay"
JOIN payment pay ON cus.customer_id = pay.customer_id;
```

```sql
USE sakila;

SELECT 
  cus.customer_id,
  cus.first_name,
  cus.last_name,
  adr.address,
  pay.rental_id, 
  pay.amount
FROM customer cus
-- juntando mais de uma tabela
JOIN payment pay
  ON cus.customer_id = pay.customer_id
JOIN address adr
  ON cus.address_id = adr.address_id;
```

## RIGHT JOIN e LEFT JOIN
Quando usamos um "JOIN" simples (também conhecido como "INNER JOIN"), a consulta retorna apenas os registros que possuem correspondência nas duas tabelas. No exemplo acima, apenas os registros onde o ID de endereço da tabela "customer" corresponde a um ID de endereço na tabela "address" serão retornados. Os registros que não têm correspondência são excluídos do resultado. Já com o "RIGHT JOIN", descrito abaixo, é retornado todos os registros da tabela da direita (tabela "address") e os registros correspondentes da tabela da esquerda (tabela "customer"). Se não houver correspondência para um registro da tabela da direita, os valores da tabela da esquerda serão nulos (NULL) para os campos selecionados. Ou seja, todos os registros da tabela "address" serão retornados, independentemente de terem ou não uma correspondência na tabela "customer". Portanto, a consulta está retornando todos os registros da tabela "address"  (completos) e os registros correspondentes da tabela "customer". O resultado incluirá o ID do cliente, o primeiro nome, o sobrenome, o endereço, o ID do aluguel e o valor do pagamento.

```sql
USE sakila;

SELECT 
  cus.customer_id,
  cus.first_name,
  cus.last_name,
  adr.address,
  pay.rental_id, 
  pay.amount
FROM customer cus
-- juntando mais de uma tabela
JOIN payment pay
  ON cus.customer_id = pay.customer_id
RIGHT JOIN address adr
  ON cus.address_id = adr.address_id;
```

## UNION
O operador UNION combina os resultados de duas ou mais queries em um único result set, retornando todas as linhas pertencentes a todas as queries envolvidas na execução. Para utilizar o UNION, o número e a ordem das colunas precisam ser idênticos em todas as queries e os data types precisam ser compatíveis. 

O operador UNION, por default, executa o equivalente a um SELECT DISTINCT no result set final. Em outras palavras, ele combina o resultado de execução das duas queries e então executa um SELECT DISTINCT a fim de eliminar as linhas duplicadas. Este processo é executado mesmo que não hajam registros duplicados.

```sql
USE sakila;

SELECT 
    cus.customer_id,
    cus.first_name,
    cus.last_name,
    adr.address,
    pay.rental_id,
    pay.amount,
    'VIP' AS Status 
FROM customer cus
JOIN payment pay
    ON cus.customer_id = pay.customer_id
JOIN address adr 
    ON cus.address_id = adr.address_id
WHERE pay.amount >= 10.99

UNION

SELECT 
    cus.customer_id,
    cus.first_name,
    cus.last_name,
    adr.address,
    pay.rental_id,
    pay.amount,
    'NON VIP' AS Status
FROM customer cus
JOIN payment pay
    ON cus.customer_id = pay.customer_id
JOIN address adr 
    ON cus.address_id = adr.address_id
WHERE pay.amount < 10.99;
```

## INSERT - Inserção de dados em uma tabela
```sql
USE sakila;

INSERT INTO language
VALUES 
	(DEFAULT, 'Portuguese', '2008-02-10 05:02:19'),
  (DEFAULT, 'Spanish', '2010-08-30 10:02:11'),
  (DEFAULT, 'Polish', '2012-02-16 12:02:02');
```

```sql
USE sakila;

-- inserção de dados em mais de uma tabela
INSERT INTO country
VALUES 
	(DEFAULT, 'Brazil2', '2022-02-15 04:44:00');
    
INSERT INTO city
VALUES 
	(DEFAULT, 'Rio grande do sul2', last_insert_id(), '2022-02-15 04:44:00');
```

## CREATE - Backup de uma tabela
```sql
USE sakila;

CREATE TABLE payment_backup AS
SELECT * FROM payment;
```

## TRUNCATE - Exclusão dos registros da tabela
```sql
USE sakila;

TRUNCATE TABLE payment_backup;
```

## DROP - Exclusão da tabela
```sql
USE sakila;

DROP TABLE payment_backup;
```

## UPDATE - Alteração de valores da tabela
```sql
USE sakila;

UPDATE payment
SET 
	amount = 15.99
WHERE
	payment_id = 1;
```

## DELETE - Exclusão de determinados registros da tabela
```sql
USE sakila;

DELETE FROM payment 
WHERE payment_id = 16049;
```

## Funções
```sql
USE sakila;

SELECT
  MIN(amount) AS Menor,
  MAX(amount) AS Maior,
  AVG(amount) AS Média
FROM payment;
```

```sql
USE sakila;

SELECT
  MIN(amount) AS Menor,
  MAX(amount) AS Maior,
  AVG(amount) AS 'Média de Valores',
  SUM(amount) AS 'Total de Vendas',
  COUNT(amount) AS 'Número de Vendas'
FROM payment
WHERE staff_id = 2;
```

## GROUP BY
O banco de dados agrupa os registros com base nos valores especificados no "GROUP BY" e, em seguida, aplica as funções de agregação para calcular os resultados para cada grupo. O resultado final é uma única linha para cada grupo com os valores agregados.

```sql
USE sakila;

SELECT 
  payment.customer_id AS ID,
  customer.first_name AS Nome,
  customer.last_name AS Sobrenome,
  SUM(amount) AS Total,
  COUNT(amount) AS Compras
FROM payment
-- Mesmo que "JOIN customer ON payment.customer_id = customer.customer_id"
JOIN customer USING (customer_id)
GROUP BY payment.customer_id
-- filtro semelhante ao 'WHERE' - seu uso se torna necessário em alguns casos, como este
HAVING Total >= 150 AND Compras >= 35
ORDER BY Total DESC;
```

## SubQuery
Uma Subquery, também conhecida como subconsulta ou subselect, é uma consulta SQL que é aninhada dentro de uma consulta principal.

```sql
USE sakila;

SELECT *
FROM payment
WHERE amount > (SELECT AVG(amount) FROM payment)
ORDER BY amount ASC;
```

```sql
USE sakila;

SELECT * 
FROM payment 
WHERE amount = 
	(SELECT MAX(amount) 
	FROM payment 
	WHERE customer_id = 2);
```

```sql
USE sakila;

SELECT *
FROM customer
WHERE customer_id IN
	(SELECT
		customer_id
	FROM payment
	GROUP BY customer_id
	HAVING COUNT(amount) > 35);
```

## Views
A View é uma representação virtual de uma ou mais tabelas em um banco de dados. Ela é criada a partir de uma consulta SQL que seleciona colunas específicas ou combina dados de uma ou mais tabelas em uma única estrutura lógica.

Em outras palavras, uma view é uma consulta armazenada que pode ser tratada como uma tabela virtual. Ela não possui dados físicos associados a ela; em vez disso, sempre que a view é consultada, os dados são obtidos diretamente das tabelas subjacentes conforme definido pela consulta de criação da view.

```sql
USE sakila;

-- Criação da view
CREATE OR REPLACE VIEW vendas_por_cliente AS
SELECT
		customer.customer_id,
    customer.first_name,
    customer.last_name,
    payment.amount
FROM customer
JOIN payment
	ON customer.customer_id = payment.payment_id;
```

```sql
USE sakila;

-- Exclusão da view
DROP VIEW vendas_por_cliente;
```

## Funções para Strings
Abaixo podemos ver alguns exemplos de funções utilizadas para manipular Strings.


```sql

-- Remover os espaços do início e fim da string (esquerda/direita)
SELECT TRIM('   Carros   ');

-- Remover os espaços do início da string (esquerda)
SELECT LTRIM('   Carros   ');

-- Remover os espaços do fim da string (direita)
SELECT RTRIM('   Carros   ');

-- Remover as letras "a" do início e fim da string (esquerda/direita)
SELECT TRIM(BOTH 'a' FROM 'aaaCarrosaaa');

-- Remover as letras "a" do início da string (esquerda)
SELECT TRIM(LEADING 'a' FROM 'aaaCarrosaaa');

-- Remover as letras "a" do fim da string (direita)
SELECT TRIM(TRAILING 'a' FROM 'aaaCarrosaaa');

-- Localizar a posição da letra "o" na string
SELECT LOCATE('o', 'Carros');

-- Alterar a string para lower case
SELECT LCASE('Carros');

-- Alterar a string para upper case
SELECT UCASE('Carros');

-- Verificar o tamanho da string
SELECT LENGTH('Carros');

-- Repetir a string 4x
SELECT REPEAT('Carros', 4);

-- Escrever as 4 primeiras letras da string (esquerda)
SELECT LEFT('Carros', 4);

-- Escrever as 4 últimas letras da string (direita)
SELECT RIGHT('Carros', 4);

-- Exemplo: em lower case, consultar o 'first_name' de todos os clientes
SELECT 
	LCASE(first_name)
FROM customer;
```

## Databases

```sql
-- Exclusão do database 'sakila'
DROP DATABASE sakila;
```

```sql
-- Criação do database 'carros'
CREATE DATABASE carros;
```

```sql
USE carros;

-- Criação da tabela 'marcas' e inserção de dados na mesma
CREATE TABLE marcas (
	id INT NOT NULL AUTO_INCREMENT,
    nome_marca VARCHAR(255) NOT NULL,
    PRIMARY KEY (id)
);
```

```sql
USE carros;

-- Adição da coluna 'origem' na tabela 'marcas'
ALTER TABLE marcas ADD origem VARCHAR(255);
```