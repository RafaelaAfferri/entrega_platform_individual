# Cache com Redis

Para melhorar o desempenho das consultas por ID nos microsserviços, foi utilizado **Redis** como mecanismo de cache.

---

## Visão Geral

Ao buscar repetidamente por entidades específicas (como produtos, contas ou pedidos) por seu **ID**, o sistema consultava diretamente o banco de dados. Com o uso do Redis, as respostas para essas requisições passam a ser armazenadas em cache, o que reduz a carga no banco e acelera o tempo de resposta.

---

## Onde o Cache foi Aplicado

O cache com Redis foi implementado nos seguintes microsserviços:

- **Product Service**: busca por produto via `/product/{id}`
- **Account Service**: busca por conta com base no usuário e senha enviado em `/account/login"`
- **Order Service**: busca por pedido via `/order/{id}`

> A lógica do cache foi aplicada apenas para requisições `GET` que utilizam o ID como chave única.

---

## Funcionamento

1. Quando uma requisição `GET /entidade/{id}` é feita:
   - O serviço verifica se a entidade com o `id` já está no Redis.
   - Se estiver, retorna o valor diretamente do cache (resposta rápida).
   - Se não estiver, consulta no banco de dados, armazena no Redis e retorna a resposta ao cliente.

2. Se a entidade for atualizada ou removida, o cache é invalidado automaticamente ou expira conforme o tempo de vida definido.

---

## Configuração (Spring Boot + Redis)

Nos arquivos de configuração do Spring Boot, foram adicionadas as seguintes linhas para habilitar o cache com Redis:

```yaml
spring:
  cache:
    type: redis
```

### Anotações nas classes Java

Para habilitar o cache nas classes de serviço, foram utilizadas anotações que seguem este padrão:

```java
@Cacheable("productId")
    public Product findById(String id) {
        return productRepository.findById(id).get().to();
    }
```


---


## Tecnologias Utilizadas

- **Spring Cache**
- **Redis** (como store de cache)
- **Docker** para executar o Redis localmente em container

---
