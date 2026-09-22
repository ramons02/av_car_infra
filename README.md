# av_car_infra — Variáveis de Ambiente

Pasta centralizada de configuração por ambiente do **AV-CAR**. Contém o arquivo `.env` com todas as variáveis usadas pela aplicação.

## Arquivo `.env`

```dotenv
# Banco de Dados (PostgreSQL)
DB_HOST=localhost
DB_PORT=5432
DB_NAME=avcar
DB_URL=jdbc:postgresql://localhost:5432/avcar
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_DRIVER=org.postgresql.Driver

# Spring Boot / Server
SERVER_PORT=8080

# Jackson / Datas
JACKSON_DATE_FORMAT=yyyy-MM-dd
JACKSON_TIME_ZONE=America/Sao_Paulo

# Java / Aplicacao
JAVA_JVM_OPTS=-Xms256m -Xmx1024m
SWING_HEADLESS=false
```

## Como é carregado

A `av_car_app` usa a biblioteca **springdotenv** (`springboot3-dotenv`). No `application.yml` há:

```yaml
springdotenv:
  directory: ../av_car_infra
  filename: .env
```

E os valores são consumidos com placeholders + fallback, ex.:

```yaml
spring:
  datasource:
    url: jdbc:postgresql://${DB_HOST:localhost}:${DB_PORT:5432}/${DB_NAME:avcar}
```

**Prioridade:** variáveis de ambiente reais do sistema operacional sempre vencem o `.env` (segurança em produção). O `.env` é somente conveniência de desenvolvimento.

## Atenção

* Não commitar o `.env`. Em um repositório, versionar um `.env.example` como referência.
* Ao alterar o `.env`, reinicie a aplicação para aplicar as mudanças.