# oleiloeiroonline

> Plataforma de leilões desenvolvida utilizando arquitetura de microsserviços, mensageria assíncrona, API Gateway e observabilidade.

## 📖 Sobre o Projeto

O **oleiloeiroonline** é um ecossistema composto por diversos microsserviços independentes, cada um responsável por um domínio específico da aplicação.

A arquitetura foi projetada seguindo princípios como:

* Arquitetura de Microsserviços
* Comunicação síncrona via APIs
* Comunicação assíncrona através de Message Broker
* API Gateway
* Observabilidade
* Baixo acoplamento
* Alta coesão

---

# 🏗 Arquitetura

```text
                        Clientes
                           │
                           ▼
                    ┌────────────────┐
                    │  API Gateway   │
                    └────────────────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        ▼                  ▼                  ▼

 User Service      Auction Service     Listing Service
        │                  │                  │
        ├──────────┐       │                  │
        ▼          ▼       ▼                  ▼

Payment      Transaction  Review        Report
 Service        Service   Service       Service

        │
        ▼

Notification Service

        ▲
        │
 Message Broker (Eventos)

        │
        ▼

Observabilidade
```

---

# 📦 Repositórios

| Serviço                  | Descrição                                                                                          |
| ------------------------ | -------------------------------------------------------------------------------------------------- |
| **API Gateway**          | Porta de entrada da aplicação. Responsável pelo roteamento das requisições para os microsserviços. |
| **User Service**         | Gerenciamento de usuários, autenticação e informações cadastrais.                                  |
| **Auction Service**      | Responsável pelas regras de negócio relacionadas aos leilões.                                      |
| **Listing Service**      |                                            |
| **Review Service**       |                                                  |
| **Payment Service**      | Processamento dos pagamentos da plataforma.                                                        |
| **Transaction Service**  |                                                                |
| **Notification Service** | Envio de notificações e comunicação com usuários.                                                  |
| **Report Service**       |                                                                 |
| **Q&A Service**          | Sistema de perguntas e respostas relacionadas aos anúncios.                                        |
| **Message Broker**       | Comunicação assíncrona entre os microsserviços.                                                    |
| **Observabilidade**      | Monitoramento, métricas, logs e rastreamento distribuído.                                          |

---

# 🔗 Estrutura dos Repositórios

```
PB Softwares Escaláveis
│
├── api-gateway
├── auction-service
├── listing-service
├── user-service
├── payment-service
├── transaction-service
├── notification-service
├── report-service
├── review-service
├── Q-AService
├── message-broker
└── observabilidade
```

---

# 🔄 Fluxo Geral

```text
Cliente

      │

      ▼

API Gateway

      │

      ├────────► User Service
      │
      ├────────► Auction Service
      │
      ├────────► Listing Service
      │
      ├────────► Payment Service
      │
      ├────────► Review Service
      │
      ├────────► Report Service
      │
      └────────► Notification Service

                 │
                 ▼

          Message Broker

                 │

                 ▼

      Comunicação Assíncrona
```

---

# 🚀 Principais Características

* Microsserviços independentes
* Comunicação síncrona e assíncrona
* API Gateway
* Mensageria baseada em eventos
* Observabilidade centralizada
* Separação por domínio de negócio
* Facilidade para manutenção e evolução

---

# 📡 Comunicação entre Serviços

A comunicação ocorre de duas formas:

### Comunicação síncrona

* HTTP/REST
* API Gateway → Microsserviços

### Comunicação assíncrona

* Eventos publicados no Message Broker
* Consumidores desacoplados
* Processamento assíncrono

---

# 📈 Observabilidade

O projeto possui um módulo dedicado para monitoramento da infraestrutura e dos serviços, incluindo:

* Centralização de logs
* Coleta de métricas
* Dashboards
* Rastreamento distribuído (Tracing)
* Monitoramento da saúde dos serviços

---

# 🎯 Objetivos da Arquitetura

* Alta disponibilidade
* Facilidade de manutenção
* Escalabilidade
* Independência entre serviços
* Resiliência
