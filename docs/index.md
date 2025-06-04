# Entrega Atividade Individual Rafaela Afférri

<!-- 
???+ info inline end "Edição"

    2025.1 -->

Este projeto implementa uma API REST em Java com Spring Boot baseada nos exercícios da [Plataform Insper](https://insper.github.io/platform/). A API oferece funcionalidades como autenticação, cadastro de usuários e cadastro de Produtos

**Aluna:** Rafaela Afferri  
**Curso:** Ciências da Computação  
**Professor:** Humberto Sandmann



<!-- 
!!! tip "Instruções"

    Vocês devem utilizar este template como um bloco de notas para registrar o que foi feito e o que falta fazer. Vocês devem adicionar as informações necessárias.
    O template deve ser editado e atualizado a cada entrega, registrando assim a data de entrega e o que foi feito até o momento via Git. -->

## Arquitetura baseada em Microsserviços

Este projeto foi desenvolvido seguindo a arquitetura de **microsserviços**, onde cada funcionalidade principal do sistema está desacoplada em um serviço independente. Os microsserviços implementados foram:

- **Product:** gerenciamento de produtos disponíveis na plataforma.
- **Order:** responsável pela criação e controle de pedidos.
- **Exchange:** Realiza conversão de câmbio de moedas
- **Auth:** autenticação e autorização de usuários.
- **Account:** gerenciamento de informações de conta dos usuários.

Todos os microsserviços são acessados por meio de um **API Gateway**, que centraliza as requisições e encaminha para o serviço correspondente, garantindo segurança, escalabilidade e organização da comunicação entre os componentes. Você encontra mais informações sobre os microserviços e suas respectivas paginas

Os microserviços podem ser visualizados neste diagrama:

``` mermaid
flowchart LR
    subgraph api [Trusted Layer]
        direction TB
        gateway --> account
        gateway --> auth
        account --> db@{ shape: cyl, label: "Database" }
        auth --> account
        gateway --> exchange
        gateway --> product
        gateway --> order:::red
        product --> db
        order --> db
        order --> product
    end
    exchange --> 3partyapi@{label: "3rd-party API (Awsome API)"}
    internet -->|request| gateway

    classDef red fill:#fcc


```

## Repositórios do Projeto
- [Gateway](https://github.com/RafaelaAfferri/store_gateway)
- [Auth](https://github.com/RafaelaAfferri/store_auth)
- [Auth-Service](https://github.com/RafaelaAfferri/store-auth-service)
- [Account](https://github.com/RafaelaAfferri/account_store)
- [Account-Service](https://github.com/RafaelaAfferri/store_account-service)
- [Product](https://github.com/RafaelaAfferri/store_product)
- [Product-Service](https://github.com/RafaelaAfferri/store-product-service)
- [Order](https://github.com/RafaelaAfferri/store_order)
- [Order-Service](https://github.com/RafaelaAfferri/order-service)
- [Exchange](https://github.com/RafaelaAfferri/entrega_1_microservicos)
Reposotório Antigo (Antes da Separação em repositórios diferentes)
- [Platform](https://github.com/RafaelaAfferri/platform_microservicos)


## Vídeo de Demonstração da API

Video da API em funcionamento:

<iframe width="100%" height="470" src="https://www.youtube.com/embed/6WSbyoHiXQs?si=P81U6wc3atxW9C5Q" allowfullscreen></iframe>


## Referências

[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/reference/){:target='_blank'} -->