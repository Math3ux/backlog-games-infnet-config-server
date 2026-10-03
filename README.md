# Config Server - Gerenciamento Centralizado de Configurações

Este projeto atua como o servidor de configuração centralizada (**Spring Cloud Config Server**) para o ecossistema de microsserviços do sistema de gerenciamento de catálogo e backlog de jogos.

## Tecnologias Utilizadas
* **Java 21**
* **Spring Boot 3.3.2**
* **Spring Cloud Config Server (2023.0.3)**
* **Docker** (Multi-stage build com Maven e Eclipse Temurin 21 Alpine)

## Funcionamento e Arquitetura
O servidor opera na porta `8888` utilizando o perfil **`native`**, lendo os arquivos de propriedades diretamente do diretório interno `src/main/resources/config/`. Ele é responsável por distribuir dinamicamente as configurações de ambiente para os serviços clientes durante a inicialização:

* **`matheus-api`**: Aplicação principal de gerenciamento do catálogo de jogos.
* **`integracao-service`**: Microsserviço Gateway de integração com a API pública CheapShark.

## Endpoints de Consulta de Configuração
Com o servidor em execução, é possível inspecionar os contratos de configuração servidos através das seguintes rotas HTTP:

* **Configurações da API Principal (Produção):** `http://localhost:8888/matheus-api/prod`
* **Configurações da API Principal (Default):** `http://localhost:8888/matheus-api/default`
* **Configurações do Serviço de Integração:** `http://localhost:8888/integracao-service/default`

## Como Executar

### 1. Via Docker Compose (Recomendado)
Este serviço é orquestrado automaticamente pelo arquivo `docker-compose.yml` localizado na raiz do repositório principal (`matheus-api`):

    docker compose up --build

### 2. Execução Isolada via Maven
Para rodar apenas o servidor de configuração localmente na máquina:

    mvn spring-boot:run