# Desafio-M-dulo-Docker-StackX

# 📌 Desafio Módulo Docker - StackX

> **Este repositório contém a solução para o desafio do módulo Docker da StackX.**  
> O projeto está organizado em duas atividades distintas: a primeira visa a conteneirização de uma aplicação **frontend simples** utilizando o servidor **web Nginx**, e a segunda envolve a implantação da plataforma **Wiki.js**, com persistência de dados em um banco de dados PostgreSQL.





---

## 🛠 Tecnologias Utilizadas

- **Docker** 🐳
- **Docker Compose** 📦
- **Nginx** (para servir o frontend)
- **PostgreSQL** (para o banco de dados do Wiki.js)
- **Wiki.js** 📖

---

## 📂 Estrutura do Projeto

desafio-modulo-docker-stackx/
│──  /atv1 # Aplicação frontend empacotada com Docker 

│    ├── index.html 

│    ├── Dockerfile 

│    ├── README.md 

│──  /atv2 # Configuração do Wiki.js usando Docker Compose 

│    ├── docker-compose.yml 

│    ├── README.md 

│     │── README.md # Documento principal do projeto


---

## 📝 Atividade 1 -  Conteneirização de Aplicação Frontend com Nginx

### 📌 Descrição  
Nesta atividade, o objetivo é conteneirizar uma aplicação frontend simples utilizando o servidor **web Nginx**. O container criado servirá um arquivo **index.html** estático e atenderá os seguintes requisitos:

### 🔹 Configuração do Dockerfile  

```dockerfile
# Usando a imagem oficial mais leve do Nginx
FROM nginx:alpine

# Definição do diretório de trabalho
WORKDIR /app

# Copia o arquivo index.html para dentro do container
COPY index.html /usr/share/nginx/html

# Define uma variável de ambiente
ENV APP_VERSION=1.0.0

# Expõe a porta 80
EXPOSE 80

# Comando para iniciar o Nginx
CMD ["nginx", "-g", "daemon off;"]
````
# 🚀 Passos para Rodar
1. Navegue até o diretório atv1 e construa a imagem:
````
docker build -t frontend-app .
````
2. Execute o container:
````
docker run -d -p 8080:80 frontend-app
````

3. Acessar no navegador:

````
http://localhost:8080
````

A página carregada será algo como:

**Dockerized Application - Feito com ❤️ usando Docker**.

# 📝 Atividade 2 - : Implantação do Wiki.js com PostgreSQL
## 📌 Descrição

Nesta atividade, implementamos a plataforma Wiki.js utilizando um ambiente Docker composto por dois containers: um para a aplicação e outro para o banco de dados PostgreSQL.

🛠 Configuração do docker-compose.yml
```yaml
version: '3.8'

services:
  postgres:
    image: postgres:14
    container_name: wiki-db
    restart: always
    environment:
      POSTGRES_DB: wiki
      POSTGRES_USER: wiki
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - wikinet

  wiki:
    image: requarks/wiki:latest
    container_name: wiki-app
    restart: always
    ports:
      - "3000:3000"
    environment:
      DB_TYPE: postgres
      DB_HOST: wiki-db
      DB_PORT: 5432
      DB_USER: wiki
      DB_PASS: password
      DB_NAME: wiki
    networks:
      - wikinet
    depends_on:
      - postgres

networks:
  wikinet:

volumes:
  postgres_data:
```

## 🛠 2. Explicação da Configuração do docker-compose.yml
🔹 Estrutura Geral
- services → Define os serviços que serão criados.
- volumes → Mantém os dados do banco de dados persistentes.
- networks → Permite a comunicação entre containers.
## Nota: O código acima cria dois serviços:
- PostgreSQL (wiki-db): Banco de dados persistente.
- Wiki.js (wiki-app): Aplicação Wiki.js conectada ao PostgreSQL.

  🔹 Serviço: Banco de Dados PostgreSQL
   ``` postgres:
    image: postgres:14
    container_name: wiki-db
    restart: always
    environment:
      POSTGRES_DB: wiki
      POSTGRES_USER: wiki
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - wikinet
   ```
  
✅ Usa a imagem oficial postgres:14.

✅ Define um banco de dados chamado wiki.

✅ Define o usuário e a senha de acesso.

✅ Define credenciais de acesso (POSTGRES_USER, POSTGRES_PASSWORD).

✅ Cria um volume chamado postgres_data para persistência.

✅ Usa uma rede chamada wikinet para comunicação entre os containers.

🔹 Serviço: Aplicação Wiki.js
 ``` wiki:
    image: requarks/wiki:latest
    container_name: wiki-app
    restart: always
    ports:
      - "3000:3000"
    environment:
      DB_TYPE: postgres
      DB_HOST: wiki-db
      DB_PORT: 5432
      DB_USER: wiki
      DB_PASS: password
      DB_NAME: wiki
    networks:
      - wikinet
    depends_on:
      - postgres
 ```
✅ Usa a imagem requarks/wiki:latest.

✅ Expõe a aplicação na porta 3000.

✅ Se conecta ao banco de dados PostgreSQL e wiki-db.

✅ depends_on: postgres → Garante que o banco inicie antes da aplicação.



# 🚀 Passos para Rodar
1 . Navegue até o diretório atv2 e execute o seguinte comando:
   
   ```` docker-compose up -d````

2 . Acessa a plataforma no navegador:
   
 ````http://localhost:3000````

## 5. Configurar o Wiki.js
- Escolher o idioma

- Criar a conta de administrador

- Configurar o banco de dados (já pré-definido no Compose)

## 📌 Comandos úteis para gerenciamento de containers

- Verificar os containers em execução:
  
  ````docker ps````
  
- Parar um container:
  
  ```` docker stop <container_id>````
  
- Verificar logs de um container:
  
  ```` docker logs <container_id> ````
  
- Remover um container:
  
  ```` docker rm <container_id> ````
  
- Remover todas as imagens:
  
  ```` docker system prune -a ````
  

# 🏆 Conclusão
Este desafio permitiu a prática da containerização de aplicações web e o uso do Docker Compose para gerenciar múltiplos containers. Com isso, aprendemos a: 

✅ Criar um container para uma aplicação frontend estática.

✅ Configurar um serviço completo com banco de dados e aplicação.

✅ Trabalhar com variáveis de ambiente no Docker.

✅ Utilizar volumes e redes para comunicação entre containers.

# 📜 Licença
Este projeto foi desenvolvido para fins educacionais como parte do curso StackX. Sinta-se à vontade para contribuir e expandir as funcionalidades!


---

### 🔹 Como este README foi estilizado?
- **Títulos grandes:** `#`, `##`, `###`
- **Blocos de código:** ```sh```, ```yaml```, ```dockerfile```
- **Citações:** `> texto`
- **Negrito:** `**texto**`
- **Listas e estrutura de diretórios:** `-`, `1.`, e ` ``` `




