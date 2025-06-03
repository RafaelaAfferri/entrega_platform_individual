
# Microsserviço de Pedidos (Order)

Este microsserviço é responsável por registrar, consultar e listar os pedidos realizados pelos usuários da plataforma.

---

## Visão Geral

O serviço de pedidos é dividido em duas partes principais:

- **Interface:** Localizada no seguinte [Repositório](https://github.com/RafaelaAfferri/store_order), define o contrato da API e os DTOs (Data Transfer Objects). Ela contém:

    - `OrderController.java`: define as rotas públicas do microsserviço de pedidos.
    - `OrderIn.java`: define o DTO de entrada para criação de pedidos.
    - `OrderOut.java`: define o DTO de saída com os dados retornados.
    - `ItemIn.java` / `ItemOut.java`: DTOs auxiliares para representar os itens do pedido.

- **Service:** Localizado no seguinte [Repositório](https://github.com/RafaelaAfferri/order-service), contém a lógica de negócio de pedidos. Os principais arquivos são:

    - `OrderApplication.java`: classe principal que inicia o serviço.
    - `Order.java`: classe correspondente à entidade de pedido.
    - `Item.java`: entidade representando um item dentro de um pedido.
    - `OrderModel.java` / `ItemModel.java`: modelos de dados persistentes.
    - `OrderRepository.java` / `ItemRepository.java`: interfaces de persistência.
    - `OrderService.java`: contém a lógica de criação e recuperação de pedidos.
    - `OrderParser.java`: faz a conversão entre DTOs e entidades.
    - `OrderResource.java`: implementa os endpoints definidos na interface `OrderController`.

---

## Principais Rotas da API Order

| Método | Rota                  | Descrição                                            |
|--------|-----------------------|------------------------------------------------------|
| POST   | [`/order`](#criar-pedido)         | Cria um novo pedido para um usuário                 |
| GET    | [`/order`](#listar-pedidos)       | Lista todos os pedidos de um usuário                |
| GET    | [`/order/{id}`](#buscar-pedido-por-id)  | Retorna os dados de um pedido específico por ID     |

---

## Exemplos de Uso

### Criar Pedido

**Endpoint:** `/order`  

**Método:** `POST`  

**Cabeçalho:**
```
id-account: 1234
```

**Corpo da Requisição:**
```json
{
  "items": [
    {
      "idProduct": "abc123",
      "quantity": 2
    },
    {
      "idProduct": "xyz456",
      "quantity": 1
    }
  ]
}
```

**Resposta:**
```json
{
    "id": "86e9badd-dab1-4352-9f9d-d8cc1c939da5",
    "date": "2025-06-03T18:14:01.085+00:00",
    "items": [
        {
            "id": "abf0b165-aa83-451f-88eb-9a2eab701a5b",
            "product": {
                "id": "a731202b-4deb-44be-b23f-4c381eff23ac",
                "name": null,
                "price": null,
                "unit": null
            },
            "quantity": 2,
            "total": 4.0
        },
        {
            "id": "c2f0b165-aa83-451f-88eb-9a2eab701a5c",
            "product": {
                "id": "b731202b-4deb-44be-b23f-4c381eff23ad",
                "name": null,
                "price": null,
                "unit": null
            },
            "quantity": 1,
            "total": 2.0
        }
    ],
    "total": 6.0
}
```

---

### Listar Pedidos

**Endpoint:** `/order`  
**Método:** `GET`  
**Cabeçalho:**
```
id-account: 1234
```

**Resposta:**
```json
[
  {
    "id": "order789",
    "items": [
      {
        "idProduct": "abc123",
        "quantity": 2
      }
    ],
    "idAccount": "1234",
    "date": "2025-06-03T12:00:00Z"
  }
]
```

---

### Buscar Pedido por ID

**Endpoint:** `/order/{id}`  
**Método:** `GET`  
**Exemplo:** `/order/order789`  
**Cabeçalho:**
```
id-account: 1234
```

**Resposta:**
```json
[
    {
        "id": "86e9badd-dab1-4352-9f9d-d8cc1c939da5",
        "date": "2025-06-03T00:00:00.000+00:00",
        "items": [],
        "total": 6.0
    }
]
```

---

## Armazenamento de Dados

Os pedidos e itens são armazenados em um banco de dados PostgreSQL. A estrutura de tabelas é definida nos arquivos de migração e contém os seguintes campos principais:

### Tabela `order`


campo | tipo | descrição
--- | --- | ---
id_order | VARCHAR(36) | Identificador único do pedido
id_account | VARCHAR(36) | ID do usuário que realizou o pedido
dt_date | DATE | Data de criação do pedido
nr_total | DECIMAL(10, 2) | Valor total do pedido


### Tabela `item`

campo | tipo | descrição
--- | --- | ---
id_item | VARCHAR(36) | Identificador do item
id_order | VARCHAR(36) | Referência ao pedido
id_product | VARCHAR(36) | Produto relacionado
nr_quantity | INT | Quantidade solicitada
nr_total | DECIMAL(10, 2) | Valor total do item


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

---
