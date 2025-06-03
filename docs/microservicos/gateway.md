# API Gateway

O **API Gateway** é o ponto de entrada principal da plataforma. Ele atua como um intermediário entre os clientes (frontend, mobile, etc.) e os microsserviços da arquitetura.

---

## Visão Geral

O gateway é responsável por:

- Centralizar e rotear requisições para os serviços apropriados (ex: `/auth`, `/product`, `/order`, etc.).
- Aplicar filtros de segurança, como autenticação e CORS.
- Expor informações básicas sobre o ambiente com o endpoint `/info`.

---

## Estrutura do Projeto

Repositório: [store_gateway](https://github.com/RafaelaAfferri/store_gateway)

### Principais Arquivos

- `GatewayApplication.java`: classe principal que inicializa o Spring Boot Gateway.
- `GatewayResource.java`: expõe um endpoint `/info` para verificar informações da máquina em execução.
- `security/AuthorizationFilter.java`: filtro que verifica se a requisição possui o header de autenticação adequado (`id-account`) antes de encaminhar para os serviços protegidos.
- `security/CorsFilter.java`: aplica política de CORS, liberando chamadas do frontend.
- `security/RouterValidator.java`: define quais rotas precisam de autenticação.
- `security/TokenOut.java` / `SolveOut.java`: DTOs auxiliares para comunicação com o serviço de autenticação.

---

## Roteamento e Segurança

O gateway utiliza filtros customizados para proteger rotas:

- **Rotas públicas** como `/auth/login` e `/auth/register` não exigem autenticação.
- **Rotas privadas** como `/order`, `/account/whoami` ou `/product` exigem o cabeçalho `id-account`.

### Exemplo de cabeçalho de autenticação
```
id-account: 1234
```

Se o header estiver ausente em uma rota protegida, o gateway retorna um erro `403 Forbidden`.

---

## Endpoint `/info`

O endpoint `/info` pode ser acessado em:

```
GET /info
```

### Exemplo de resposta:
```json
{
  "hostname": "gateway-container",
  "os.arch": "amd64",
  "os.name": "Linux",
  "os.version": "5.10.0-23-amd64"
}
```

Este endpoint é útil para depuração e verificação da infraestrutura em tempo real (por exemplo, em ambientes com múltiplos pods Kubernetes).

---

## Tecnologias Utilizadas

- **Java 21**
- **Spring Boot 3**
- **Spring Cloud Gateway**
- **Spring Security (filtros personalizados)**
- **Docker** e **Kubernetes (k8s)**
- **Jenkins** para integração contínua

---
