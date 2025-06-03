# Microsserviço de Conta (Account)

Este microsserviço é responsável pela criação, autenticação e recuperação de informações das contas de usuário na plataforma.

---

## Visão Geral

O serviço de contas é dividido em duas partes principais:

- **Interface:** Localizada no seguinte [Repositório](https://github.com/RafaelaAfferri/account_store), define o contrato da API e os DTOs (Data Transfer Objects). Ela contém:

    - `AccountController.java`: define as rotas públicas do microsserviço de conta.
    - `AccountIn.java`: define o DTO de entrada para criar ou autenticar uma conta.
    - `AccountOut.java`: define o DTO de saída com os dados da conta retornados para o cliente.

- **Service:** Localizado no seguinte [Repositório](https://github.com/RafaelaAfferri/store_account-service), contém a lógica de negócio relacionada às contas, incluindo criação, login e identificação de usuários. Os principais arquivos são:

    - `AccountApplication.java`: classe principal que inicia o serviço.
    - `Account.java`: classe correspondente à entidade de conta, representando os dados persistidos.
    - `AccountModel.java`: modelos de dados a serem utilizados pelo banco de dados.
    - `AccountRepository.java`: interface que lida com a persistência de dados usando Spring Data.
    - `AccountService.java`: contém as regras de negócio de contas (criar, autenticar, listar, etc.).
    - `AccountParser.java`: faz a conversão entre DTOs e entidades.
    - `AccountResource.java`: implementa os endpoints definidos na interface `AccountController`.

---

## Principais Rotas da API Account

| Método | Rota               | Descrição                                       |
|--------|--------------------|-------------------------------------------------|
| POST   | [`/account`](#criar-conta)        | Cria uma nova conta de usuário                 |
| GET    | [`/account`](#listar-contas)         | Lista todas as contas registradas             |
| POST   | [`/account/login`](#buscar-conta-autenticar)   | Busca conta por e-mail e senha (autenticação) |
| GET    | [`/account/whoami`](#identificar-conta)  | Retorna dados da conta com base no ID enviado |

---

## Exemplos de Uso

### Criar Conta

**Endpoint:** `/account`  

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
    "id": "1234",
    "name": "Rafaela",
    "email": "rafaela@insper.edu.br",
}
```

### Listar Contas
**Endpoint:** `/account`

**Método:** `GET`

**Resposta:**
```json
[
    {
        "id": "1234",
        "name": "Rafaela",
        "email": "rafaela@insper.edu.br"
    },
    {
        "id": "5678",
        "name": "João",
        "email": "joado@insper.edu.br",
    },
]

```

### Buscar Conta (Autenticar)
**Endpoint:** `/account/login`

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
    "id": "1234",
    "name": "Rafaela",
    "email": "rafaela@insper.edu.br"
}
```

### Identificar Conta
**Endpoint:** `/account/whoami`

**Método:** `GET`

**Cabeçalho da Requisição:**
```Authorization
id-account: 1234
```

**Resposta:**
```json
{
    "id": "1234",
    "name": "Rafaela",
    "email": "rafaela@insper.edu.br"
}
```
---

## Armazenamento de Dados
Os dados das contas são armazenados em um banco de dados PostgreSQL, que é configurado no arquivo separadamente, mas pode ser encontrado no arquivo `compose.yaml` neste [Repositório](https://github.com/RafaelaAfferri/platform_microservicos). A tabela por outro lado é configurada no arquivos encontrados no caminho `src\main\resources\db\migration` e contém os seguintes campos:

campo | Tipo | Descrição
--- | --- | ---
id_account | VARCHAR(36) | Identificador único da conta (UUID)
tx_name | VARCHAR(256) | Nome do usuário
tx_email | VARCHAR(256) | E-mail do usuário
tx_sha256 | VARCHAR(256) | Senha do usuário (armazenada de forma segura com hash)
dt_birthdate | DATE | Data de nascimento do usuário
dt_creation | TIMESTAMP | Data de criação da conta





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




