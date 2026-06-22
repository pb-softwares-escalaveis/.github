
# O Leiloeiro Online

> Plataforma de leilões desenvolvida utilizando arquitetura de microsserviços, mensageria assíncrona, API Gateway e observabilidade.
Mais informações podem ser encontradas no documento: https://docs.google.com/document/d/1IwLaNUv1CrFVAYuDKi700pC3CdRqt-E6lAhX_VVGOcI/edit?pli=1&tab=t.0

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

---

# 🚀 Funcionamento

Essa organização possui todos os microsserviços necessários para o funcionamento da aplicação. Você pode optar por rodar cada serviço individualmente através do docker-compose do serviço em específico ou então rodar o docker-compose presente no repositório compose-master.

> 💡 ATENÇÃO 
> Devido ao grande número de microsserviços e dependências necessárias para o funcionamento da aplicação como um todo, NÃO tente rodar o compose master caso você não disponha de pelo menos 10 GB de RAM livre. Ainda assim, o módulo de observabilidade ficou separado por conta do limite computacional atingido.

Para fazer a aplicação rodar, siga os seguintes passos:

 1. Peça o .env atualizado a um dos componentes da organização e o coloque no mesmo nível do docker-compose do projeto desejado.
 2. Certifique-se de que todos os serviços estão rodando na mesma rede interna do docker. Por padrão, no docker-compose master, eles rodam numa rede chamada leilao-network, que é criada no momento da subida dos conteineres.
 3. AGUARDE. São pelo menos 40 conteineres e muitos deles (ksqldb, elasticsearch, keycloak, kafka connect, kafka, etc) são pesados e demoram para ficar prontos.
 4. Acesse a aplicação via front-end via localhost:3000.
