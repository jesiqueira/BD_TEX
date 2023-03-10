# Instalando MySQL

### **Comandos**:

- sudo apt-get install mysql-server
- wget https://dev.mysql.com/get/mysql-apt-config_0.8.22-1_all.deb
- sudo dpkg -i mysql-apt-config\*
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
- systemctl stop mysql
- systemctl start mysql
- systemctl restart mysql
- sudo /etc/init.d/mysql stop
- sudo /etc/init.d/mysql start

# Desabilitar inicialização automática no debian
- systemctl disable mysql
  - Isso remove o link simbólico para o serviço do MySQL no diretório /etc/systemd/system/multi-user.target.wants, que é usado pelo sistema para iniciar serviços automaticamente durante a inicialização.

# INSTALAR MYSQL-WORKBENCH-COMMUNITY

- sudo apt install snapd
- sudo snap install core
- sudo snap install mysql-workbench-community

---

# CONFIGURAR MYSQL

### ALTERAR A SENHA DE USUÁRIO

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'MINHASENHASECRETA#@';

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

`create schema livraria default character set utf8mb4 colllate uft8mb4_0900_ai_ci;`

# Criar databasess.
  `CREATE SCHEMA livraria DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci;`
<!-- `create databases livraria; -->

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

`CREATE TABLE IF NOT EXISTS pedidos(
  id_pedidos integer not null,
  id_livro integer not null,
  data_hora datetime not null,
  primary key(id_pedidos)
);`

`AlTER TABLE livro CHANGE id_livro id_livro integer auto_increment`;
`INSERT INTO livro (titulo, resumo, paginas) VALUES ('neo', 'Viagem a matrix', '200');`
`UPDATE livro SET  resumo = 'Guardicao dos sonhos' WHERE id_livro=2;`

`drop data bases locadora;`

`AlTER TABLE livro CHANGE id_livro id_livro integer auto_increment;`

`ALTER TABLE pedidos ADD CONSTRAINT fk_id_livro FOREIGN KEY (id-livro) REFERENCES livro(id_livro);`

`INSERT INTO livro (titulo, resumo, paginas) VALUES ('neo', 'Viagem a matrix', '200');`

`UPDATE livro SET  resumo = 'Guardicao dos sonhos' WHERE id_livro=2;`

`drop data bases locadora;`

# INSERT

- `INSERT INTO nivel VALUES (null, 'Oficial');`
- `INSERT INTO nivel VALUES (null, 'Marujo');`
- `INSERT INTO nivel VALUES (null, 'Capitao');`
- `INSERT INTO nivel VALUES (null, 'Almirante');`


- `Insert into produto_categoria VALUES (null, 'Frutos do Mar');`
- `Insert into produto_categoria VALUES (null, 'Carnes');`
- `Insert into produto_categoria VALUES (null, 'Pastas');`
- `Insert into produto_categoria VALUES (null, 'Caldos');`
- `Insert into produto_categoria VALUES (null, 'Comida Brasileira');`

- `INSERT INTO produto_tipo VALUES (null, 'Opcional');`
- `INSERT INTO produto_tipo VALUES (null, 'Principal');`
---

# INDICES

`CREATE TABLE nomeTabela(
  c1 INT PRIMARY KEY,
  c2 INT NOT NULL,
  c3 INT NOT NULL,
  c4 VARCHAR(10),
  INDEX (C2, C3)
);`

`Adicionar um novo indice para uma tabela existente;`

`CREATE INDEX nome_do_indice ON nome_da_tabela (coluna);`

## verificar quantas linhas leu até encontrar o resultado em uma consulta sem indice, use o explain.
`EXPLAIN SELECT * FROM livro WHERE titulo='O velho e o mar';`

---
# VERIFICAR OS INDICE QUE EXISTEM EM UMA TABELA.
 - SHOW INDEXES FROM nome_da_tabela;

---
# CHECK Restrição e verificação

`CREATE TABLE usuarios(
  id_usuario INT PRIMARY KEY,
  nome VARCHAR(30) NOT NULL,
  sobrenome VARCHAR(30) NOT NULL,
  idade int,
  CHECK (idade >=16)
);`

`ALTER TABLE usuarios ADD CONSTRAINT CHK_idade CHECK (idade >= 16);`


# VIEWS

-  Visualizar descrição completa da tabela.
-  `SHOW CREATE TABLE nome_da_tabela;`

Views é uma tabela virtual resultado de outra tabela

## create view
`CREATE VIEW dias_da_semana (dias) AS
  SELECT 'Segunda'
  UNION
  SELECT 'Terca'
  UNION
  SELECT 'Quarta'
  UNION
  SELECT 'Quinta'
  UNION
  SELECT 'Sexta'
  UNION
  SELECT 'Sabado' 
  UNION
  SELECT 'Domingo'
  `

`CREATE VIEW livros_ate_100_reais AS SELECT titulo, resenha FROM livro WHERE preco <= 100;`

- Executar select na view
  - `select * from livros_ate_100_reais;`

