# Introdução

Código desenvolvido com base no Curso da udemy:
https://www.udemy.com/course/arquitetura-de-microsservicos-padrao-saga-orquestrado

Código fonte curso:
https://github.com/vhnegrisoli/curso-udemy-microsservicos-padrao-saga-orquestrado

## Tecnlogias utilizdas

- Java 21
- Spring Boot 3
- Apache Kafka
- API REST
- PostgreSQL
- MongoDB
- Docker
- docker-compose
- Redpanda Console

## Ferramentas utilizdas

- IntelliJ IDEA Community Edition
- Docker
- Maven

## Arquitetura

Em nossa arquitetura, teremos 5 serviços:

- **Order-Service:** microsserviço responsável apenas por gerar um pedido inicial, e receber uma notificação. Aqui que teremos endpoints REST para inciar o processo e recuperar os dados dos eventos. O banco de dados utilizado será o MongoDB.
- **Orchestrator-Service:** microsserviço responsável por orquestrar todo o fluxo de execução da Saga, ele que saberá qual microsserviço foi executado e em qual estado, e para qual será o próximo microsserviço a ser enviado, este microsserviço também irá salvar o processo dos eventos. Este serviço não possui banco de dados.
- **Product-Validation-Service:** microsserviço responsável por validar se o produto informado no pedido existe e está válido. Este microsserviço guardará a validação de um produto para o ID de um pedido. O banco de dados utilizado será o PostgreSQL.
- **Payment-Service:** microsserviço responsável por realizar um pagamento com base nos valores unitários e quantidades informadas no pedido. Este microsserviço guardará a informação de pagamento de um pedido. O banco de dados utilizado será o PostgreSQL.
- **Inventory-Service:** microsserviço responsável por realizar a baixa do estoque dos produtos de um pedido. Este microsserviço guardará a informação da baixa de um produto para o ID de um pedido. O banco de dados utilizado será o PostgreSQL.

Todos os serviços da arquitetura irão subir através do arquivo docker-compose.yml.


## Executando aplicação

```sh
    docker-compose up --build -d
```
