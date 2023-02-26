

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

create databases livraria;

create table livro(
  id_livro integer not null,
  titulo char(50) not null,
  resumo longtext null,
  paginas integer not null,
  primary key(id_livro)
);

create table  if not exists locadora(
  id_livro integer not null,
  titulo char(50) not null,
  resumo longtext null,
  paginas integer not null,
  primary key(id_livro)
);

AlTER TABLE livro CHANGE id_livro id_livro integer auto_increment;
INSERT INTO livro (titulo, resumo, paginas) VALUES ('neo', 'Viagem a matrix', '200');
UPDATE livro SET  resumo = 'Guardicao dos sonhos' WHERE id_livro=2;

drop data bases locadora;