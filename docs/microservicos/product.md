# Microsserviço de Produtos (Product)

Este microsserviço é responsável pelo cadastro, listagem, consulta e exclusão de produtos disponíveis na plataforma.

---

## Visão Geral

O serviço de produtos é dividido em duas partes principais:

- **Interface:** Localizada no seguinte [Repositório](https://github.com/RafaelaAfferri/store_product), define o contrato da API e os DTOs (Data Transfer Objects). Ela contém:

    - `ProductController.java`: define as rotas públicas do microsserviço de produto.
    - `ProductIn.java`: define o DTO de entrada para criação de produtos.
    - `ProductOut.java`: define o DTO de saída com os dados retornados.

- **Service:** Localizado no seguinte [Repositório](https://github.com/RafaelaAfferri/store-product-service), contém a lógica de negócio de produtos. Os principais arquivos são:

    - `ProductApplication.java`: classe principal que inicia o serviço.
    - `Product.java`: classe correspondente à entidade de produto no banco.
    - `ProductModel.java`: modelo de dados persistente.
    - `ProductRepository.java`: interface de persistência via Spring Data.
    - `ProductService.java`: contém as regras de negócio (criar, listar, buscar e deletar).
    - `ProductParser.java`: faz a conversão entre DTOs e entidades.
    - `ProductResource.java`: implementa os endpoints definidos na interface `ProductController`.

---

## Principais Rotas da API Product

| Método | Rota                   | Descrição                                      |
|--------|------------------------|-----------------------------------------------|
| POST   | [`/product`](#criar-produto)            | Cadastra um novo produto                       |
| GET    | [`/product`](#listar-produtos)          | Lista todos os produtos registrados            |
| GET    | [`/product/{id}`](#buscar-produto-por-id)      | Busca um produto específico por ID             |
| DELETE | [`/product/{id}`](#deletar-produto)     | Remove um produto com base no ID               |

---

## Exemplos de Uso

### Criar Produto

**Endpoint:** `/product`  

**Método:** `POST`  

**Corpo da Requisição:**
```json
{
  "name": "Tomate",
  "price": 12.99,
  "unit": "kg",
}
```
**Resposta:**
```json
{
  "id": "abc123",
  "name": "Tomate",
  "price": 12.99,
  "unit": "kg",
}
```

---

### Listar Produtos

**Endpoint:** `/product`  

**Método:** `GET`  

**Resposta:**
```json
[
    {
    "id": "abc123",
    "name": "Tomate",
    "price": 12.99,
    "unit": "kg",
    },
    {
    "id": "def456",
    "name": "Uva Verde",
    "price": 15.99,
    "unit": "kg",
]
```

---

### Buscar Produto por ID

**Endpoint:** `/product/{id}`  

**Método:** `GET`  

**Exemplo de chamada:** `/product/abc123`  

**Resposta:**
```json
{
  "id": "abc123",
  "name": "Tomate",
  "price": 12.99,
  "unit": "kg",
}
```

---

### Deletar Produto

**Endpoint:** `/product/{id}`  

**Método:** `DELETE`  

**Exemplo de chamada:** `/product/abc123`  

**Resposta:**
```json
{
  "id": "abc123",
  "name": "Tomate",
  "price": 12.99,
  "unit": "kg",
}
```

---

## Armazenamento de Dados

Os produtos são armazenados em um banco de dados PostgreSQL, configurado no ambiente Docker e com tabelas definidas nos arquivos de migração (`src/main/resources/db/migration`). Os campos da tabela de produtos são:

campo | Tipo | Descrição
--- | --- | ---
id_product | VARCHAR(36) | Identificador único do produto (UUID)
tx_name | VARCHAR(256) | Nome do produto
tx_price | DECIMAL(10, 20) | Preço unitário do produto
tx_unit | VARCHAR(64) | Unidade de medida do produto (ex: kg, unidade)
---

## Tecnologias Utilizadas

- **Java 21**
- **Spring Boot 3**
- **Spring Web / REST**
- **Spring Data JPA**
- **PostgreSQL** como banco de dados
- **Maven** como gerenciador de dependências
- **Docker** e **Kubernetes (k8s)** para orquestração
- **Jenkins** para integração contínua
