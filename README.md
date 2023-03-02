

# Instalando MySQL

### **Comandos**:
  - sudo apt-get install mysql-server
  - wget https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb
  - sudo dpkg -i mysql-apt-config*
  - sudo apt update
  - sudo apt install mysql-server

### **Visualizar versão**:
  - mysql --version 

### **Verificar se serviço está ativo**:
  - systemctl is-active mysql
  - sudo systemctl status mysql

### SAIR DO MYSQL
- quit

# STOP/START/RESTART SERVIDOR MYSQL
- sudo /etc/init.d/mysql stop
- sudo /etc/init.d/mysql start
- systemctl restart mysql
  
# INSTALAR MYSQL-WORKBENCH-COMMUNITY
- sudo apt install snapd
- sudo snap install core
- sudo snap install mysql-workbench-community
---


# CONFIGURAR MYSQL

### ALTERAR A SENHA DE USUÁRIO
ALTER USER 'root'@'localhost' IDENTIFIED WITH  mysql_native_password BY 'MINHASENHASECRETA#@';

### ACESSAR BD
- sudo mysql (quando não tem senha)
- mysql -u root -p (quando tem senha)


# UTILIZANDO O MYSQL

### visualizar todas as tabelas`
- show databases
- show tables
- use nomeDatabase

### Descrever tabelas
- describe user;
- describe nomeTabela

  
# VERIFICAR ENGINES MYSQL
- show engines;
- TIPOS DE MOTORES:
  - ISAM(descontinuado)
  - MyISAM
  - MERGE
  - InnoDB (Default)
  - MEMORY (HELP)
  - ARCHIVE
  - BDB
  - CSV
  - FEDERATED
  
  # Camandos SQL

  create schema `livraria` default character set utf8mb4 colllate uft8mb4_0900_ai_ci;

# Criar databasess.
  - CREATE SCHEMA livraria DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;
<!-- create databases livraria; -->

# Criar tabelas
`create table if not exists livro(
  id_livro integer not null,
  titulo char(50) not null,
  resumo longtext null,
  paginas integer not null,
  primary key(id_livro)
);`

`create table  if not exists locadora(
  id_livro integer not null,
  titulo char(50) not null,
  resumo longtext null,
  paginas integer not null,
  primary key(id_livro)
);`

CREATE TABLE IF NOT EXISTS pedidos(
  id_pedidos integer not null,
  id_livro integer not null,
  data_hora datetime not null,
  primary key(id_pedidos)
);

# VISUALIZAR CAMPO DA TABELA
`DESCRIBE nomeTabela;`

# Alterar tabela

`AlTER TABLE livro CHANGE id_livro id_livro integer auto_increment;`

## ALTERAR COLUNA DA TABELA:
`ALTER TABLE livro RENAME COLUMN nomedacoluna to novoNome;`

## CRIAR NOVA COLUNA:
`ALTER TABLE livro ADD nomeDaColuna tipoDados: string/interger...;`

## REMOVER COLUNA:
`ALTER TABLE livro DROP COLUMN nomeDaColuna;`

# INSERT
`INSERT INTO livro (titulo, resumo, paginas) VALUES ('neo', 'Viagem a matrix', '200');`

`INSERT INTO livro VALUES(null,'Dory', 'O Leão Dourado', 152);`

`INSERT INTO livro VALUES(null,'Dory', 'O Leão Dourado', 152);`

`INSERT INTO livro VALUES (null, 'Burak', null, 235)`

# UPDATE
`UPDATE livro SET  resumo = 'Guardicao dos sonhos' WHERE id_livro=2;`

# DELETE
`DELETE FROM livro WHERE id_livro=2;` 

# DROP DATA BASES
`DROP SCHEMA locadora;`


# Esvaziar ou Limpar a tabela
`TRUNCATE TABLE livro;`

# ELIMINAR TABELA
`DROP TABLE livro`

# INNER JOIN
- SELECT EM 2 OU MAIS TABELAS COM INNER JOIN,
  
`select livro.titulo as tiulo_livro, locadora.nome from locadora INNER JOIN livro on livro.id_livro = locadora.id_livro;`

`SELECT l.titulo, lo.nome as locadora, p.data_hora FROM  livro l INNER JOIN locadora lo on l.id_livro = lo.id_livro INNER JOIN pedidos p ON l.id_livro = p.id_livro;`

# LEFT JOIN
`SELECT l.titulo, lo.nome as locadora, p.data_hora FROM  livro l LEFT JOIN locadora lo on l.id_livro = lo.id_livro LEFT JOIN pedidos p ON l.id_livro = p.id_livro;`

# RIGHT JOIN
` SELECT l.titulo, lo.nome as locadora, p.data_hora FROM  livro l  RIGHT JOIN locadora lo on l.id_livro = lo.id_livro  RIGHT JOIN pedidos p ON l.id_livro = p.id_livro; `

# DISTINCT
`SELECT DISTINCT t.nome FROM tabela as t INNER JOIN outraTabela as o on t.id = o.id `

# COUNT E AVERAGE
`SELECT COUNT(id_livro) as Total_livro FROM livro;`

`SELECT MIN(preco) as meno_preco FROM livro;`

`SELECT MAX(preco) as meno_preco FROM livro;`

`SELECT titulo, MIN(preco) as menor_preco FROM livro GROUP BY titulo HAVING MIN(preco) < 100;`

`SELECT AVG(preco) as preco_medio FROM livro;`
