# 🌱 Projeto - GreenFlow (Cidades ESG Inteligentes)

## 📌 Descrição

O **GreenFlow** é uma aplicação desenvolvida com foco em cidades inteligentes e sustentabilidade (ESG), permitindo monitoramento e gerenciamento de serviços urbanos de forma eficiente.

Este projeto demonstra a implementação de boas práticas DevOps, incluindo:

* Integração Contínua (CI)
* Entrega Contínua (CD)
* Containerização com Docker
* Orquestração com Docker Compose

---

## 🚀 Como executar localmente com Docker

### 🔧 Pré-requisitos

* Docker instalado
* Docker Compose instalado

### ▶️ Passos para execução

```bash
docker-compose up --build
```

### 🌐 Acessar aplicação

* API principal:

```
http://localhost:8080
```

* Health check:

```
http://localhost:8080/health
```

---

## ⚙️ Pipeline CI/CD

O pipeline foi implementado utilizando o **GitHub Actions**, automatizando todo o fluxo de integração e deploy.

### 🔄 Funcionamento

A cada push no repositório:

1. O código é automaticamente validado
2. A aplicação é compilada (build)
3. Os testes automatizados são executados
4. A imagem Docker é gerada
5. O deploy é executado conforme o ambiente

### 🌍 Ambientes

* **Staging**

  * Branch: `develop`
  * Objetivo: testes e validação

* **Produção**

  * Branch: `main`
  * Objetivo: versão final da aplicação

---

## 🐳 Containerização

A aplicação foi containerizada utilizando Docker.

### 📦 Estratégias adotadas

* Uso de **multi-stage build** para reduzir o tamanho da imagem
* Separação de serviços (aplicação e banco)
* Uso de variáveis de ambiente
* Persistência de dados com volumes

---

## 📄 Dockerfile

```dockerfile
FROM maven:3.9.6-eclipse-temurin-17 AS build

WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

FROM openjdk:17-jdk-slim

WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

## 🧩 Orquestração (Docker Compose)

```yaml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "8080:8080"
    depends_on:
      - db
    environment:
      SPRING_DATASOURCE_URL: jdbc:postgresql://db:5432/meu_banco
      SPRING_DATASOURCE_USERNAME: usuario
      SPRING_DATASOURCE_PASSWORD: senha

  db:
    image: postgres:15
    environment:
      POSTGRES_DB: meu_banco
      POSTGRES_USER: usuario
      POSTGRES_PASSWORD: senha
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

---

## 📸 Evidências de funcionamento

### 🔹 Execução local

* Aplicação rodando em `localhost:8080`
* Endpoint `/health` respondendo OK

### 🔹 Pipeline CI/CD

* Build executado com sucesso
* Testes automatizados executados
* Deploy staging realizado
* Deploy produção realizado

📌 *(Inserir prints do GitHub Actions aqui)*

---

## 🛠 Tecnologias utilizadas

* Java 17+
* Spring Boot
* Maven
* Docker
* Docker Compose
* GitHub Actions
* PostgreSQL

---

## ⚠️ Observações

* O deploy foi automatizado via pipeline CI/CD
* Ambientes staging e produção foram simulados através de branches
* A aplicação pode ser facilmente adaptada para deploy real em cloud

---

## 👨‍💻 Autores

Gustavo Giotto Avelar
Giovanni Alves Lavia
Israel Luiz Azevedo

---

## ✅ Checklist de Entrega

* [x] Projeto compactado em .ZIP com estrutura organizada
* [x] Dockerfile funcional
* [x] docker-compose.yml
* [x] Pipeline CI/CD com build, teste e deploy
* [x] README.md com instruções e evidências
* [x] Documentação técnica (PDF/PPT)
* [x] Deploy em staging e produção

---
