# Microsserviço de Autenticação (Auth)

Este microsserviço é responsável pelo controle de autenticação e autorização dos usuários da plataforma.

## Visão Geral

O serviço de autenticação é dividido em duas partes principais:

- **Interface:** Encontrado no seguinte [Repositório](https://gitub.com/RafaelaAfferri/store_auth) possui a definição do contrato da API e os modelos de DTOs (Data Transfer Objects). Ela possuí o seguintes arquivos:
    - AuthContoller.java: define a interface com as rotas da API expostas no gateway.
    - LoginIn.java: define o DTO de entrada para o login.
    - RegisterIn.java: define o DTO de entrada para o registro.
    - SolveOut.java: define o DTO de saída para a validação do token JWT.
    - TokenOut.java: define o DTO de saída para o token JWT.

- **Service:** Encontrado no seguinte [Repositório](https://github.com/RafaelaAfferri/store-auth-service), implementa a lógica de autenticação do usuário, incluindo o registro, login e validação de tokens JWT. Ele contém os seguintes arquivos:
    - AuthApplication.java: classe principal que inicia o serviço.
    - AuthParser.java: responsável por transformar os DTOs de entrada e saída.
    - AuthResource.java: implementa os endpoints definidos na interface `AuthController`.
    - AuthService.java: contém a lógica de autenticação, incluindo o registro de usuários, login e validação de tokens JWT.
    - JwtService.java: responsável pela criação e validação de tokens JWT.
    - Register.java: modelo de dados para o registro de usuários.


---

## Principais Rotas da API Auth

O controlador principal é a interface `AuthController`, cujos endpoints são implementados por `AuthResource`.

| Método | Rota           | Descrição                        |
|--------|----------------|----------------------------------|
| POST   | [`/auth/register`](#registro-de-usuário) | Cadastra um novo usuário         |
| POST   | [`/auth/login`](#login-de-usuário)    | Realiza o login do usuário       | 
| POST   | [`/auth/solve`](#validação-de-token-jwt)    | Decodifica e valida um token JWT|



## Exemplos de Uso

### Registro de Usuário

**Endpoint:** `/auth/register`

**Método:** `POST`

**Corpo da Requisição:**
```json
{
  "name": "Rafaela",
  "email": "rafaela@insper.edu.br",
  "password": "123456"
}
```

**Resposta:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```
### Login de Usuário
**Endpoint:** `/auth/login`

**Método:** `POST`

**Corpo da Requisição:**
```json
{
  "email": "rafaela@insper.edu.br",
  "password": "123456"
}
```

**Resposta:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```
### Validação de Token JWT
**Endpoint:** `/auth/solve`

**Método:** `POST`

**Corpo da Requisição:**
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Resposta:**
```json
{
  "email": "rafaela@insper.edu.br",
  "sub": "1234",
  "iat": 1717440000
}
```

---

## Tecnologias Utilizadas

- **Java 21**
- **Spring Boot 3**
- **Spring Web / REST**
- **JWT (JSON Web Token)** para autenticação stateless
- **Maven** como gerenciador de dependências
- **Docker** e **Kubernetes (k8s)** para orquestração
- **Jenkins** para integração contínua

---




