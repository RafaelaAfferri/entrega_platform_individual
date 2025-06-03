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
## Códigos

=== "De um arquivo remoto"

    ``` { .yaml .copy .select linenums='1' title="main.yaml" }
    --8<-- "https://raw.githubusercontent.com/hsandmann/documentation.template/refs/heads/main/.github/workflows/main.yaml"
    ```

=== "Anotações no código"

    ``` { .yaml title="compose.yaml" }
    name: app

        db:
            image: postgres:17
            environment:
                POSTGRES_DB: ${POSTGRES_DB:-projeto} # (1)!
                POSTGRES_USER: ${POSTGRES_USER:-projeto}
                POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-projeto}
            ports:
                - 5432:5432 #(2)!
    ```

    1.  Caso a variável de ambiente `POSTGRES_DB` não exista ou seja nula - não seja definida no arquivo `.env` - o valor padrão será `projeto`. Vide [documentação](https://docs.docker.com/reference/compose-file/interpolation/){target='_blank'}.

    2. Aqui é feito um túnel da porta 5432 do container do banco de dados para a porta 5432 do host (no caso localhost). Em um ambiente de produção, essa porta não deve ser exposta, pois ninguém de fora do compose deveria acessar o banco de dados diretamente.


## Exemplo de vídeo

Lorem ipsum dolor sit amet

<iframe width="100%" height="470" src="https://www.youtube.com/embed/3574AYQml8w" allowfullscreen></iframe>


## Referências

[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/reference/){:target='_blank'}