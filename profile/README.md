# FastFood Autoatendimento - Projeto Tech Challenge FIAP

![FIAP](https://img.shields.io/badge/FIAP-Software%20Architecture-red)
![Status](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow)
![Módulo](https://img.shields.io/badge/Módulo-4-blue)

## 📚 Sobre o Programa

Este projeto faz parte do **programa de pós-graduação lato sensu em Software Architecture da FIAP**, especificamente do curso **SOAT (Software Architecture)**, onde desenvolvemos uma solução completa de autoatendimento para lanchonetes, aplicando conceitos modernos de arquitetura de software, microsserviços, cloud computing e DevOps.

### Tech Challenge - Evolução por Fases

O projeto foi desenvolvido de forma evolutiva através de 4 fases (módulos), cada uma adicionando novos requisitos e complexidade:

- **Fase 1 (Módulo 1)**: Arquitetura monolítica com DDD, Docker e Kubernetes
- **Fase 2 (Módulo 2)**: Infraestrutura como código (Terraform) e CI/CD
- **Fase 3 (Módulo 3)**: Arquitetura serverless com AWS Lambda e escalabilidade
- **Fase 4 (Módulo 4)**: Microsserviços, mensageria e arquitetura orientada a eventos

---

## 🏗️ Arquitetura do Sistema

O sistema FastFood foi projetado seguindo princípios de **arquitetura hexagonal** (Ports and Adapters), **Domain-Driven Design (DDD)** e **microsserviços**, garantindo alta coesão, baixo acoplamento e escalabilidade.

### Visão Geral da Arquitetura

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENTE / TOTEM                          │
└────────────────────────────┬────────────────────────────────────┘
                             │
                    ┌────────▼────────┐
                    │  API Gateway    │
                    │  Load Balancer  │
                    └────────┬────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
┌───────▼────────┐  ┌────────▼────────┐  ┌───────▼────────┐
│  Lambda Auth   │  │  Order Service  │  │ Payment Service│
│   (Serverless) │  │   (Kubernetes)  │  │  (Kubernetes)  │
└───────┬────────┘  └────────┬────────┘  └───────┬────────┘
        │                    │                    │
        │           ┌────────▼────────┐           │
        │           │  CTO Service    │           │
        │           │  (Kubernetes)   │           │
        │           └────────┬────────┘           │
        │                    │                    │
        └────────────────────┼────────────────────┘
                             │
                    ┌────────▼────────┐
                    │   Amazon RDS    │
                    │   MySQL         │
                    └─────────────────┘
```

---

## 📦 Repositórios do Projeto

O projeto está organizado em múltiplos repositórios, cada um com responsabilidades específicas:

### 🍔 Aplicação Principal

#### [fast-food](https://github.com/fiap-software-architecture-tech/fast-food)
**Core da aplicação FastFood** - Repositório principal contendo a aplicação backend com todas as funcionalidades de gerenciamento de pedidos, produtos, clientes e integração com pagamentos.

- **Tecnologias**: TypeScript, Fastify, Prisma ORM
- **Arquitetura**: Hexagonal (Ports & Adapters)
- **Features**: CRUD completo, API RESTful, Swagger Documentation
- **Branch Principal**: `modulo_4`

### 🔐 Autenticação

#### [fast-food-auth](https://github.com/fiap-software-architecture-tech/fast-food-auth)
**Autenticação Serverless** - Função Lambda para autenticação de clientes via CPF com geração de tokens JWT.

- **Tecnologias**: TypeScript, AWS Lambda, API Gateway
- **Arquitetura**: Serverless, Hexagonal
- **Features**: Validação de CPF, JWT Tokens, Pay-per-request
- **Branch Principal**: `modulo_4`

### 📦 Microsserviços (Módulo 4)

#### [fast-food-order](https://github.com/fiap-software-architecture-tech/fast-food-order)
**Microsserviço de Pedidos** - Gerenciamento de pedidos com mensageria.

- **Responsabilidade**: Criação, atualização e consulta de pedidos
- **Comunicação**: Eventos assíncronos para Payment e CTO
- **Branch Principal**: `modulo_4`

#### [fast-food-payment](https://github.com/fiap-software-architecture-tech/fast-food-payment)
**Microsserviço de Pagamentos** - Processamento e validação de pagamentos.

- **Responsabilidade**: Integração com gateways de pagamento (Mercado Pago)
- **Comunicação**: Eventos de confirmação de pagamento
- **Branch Principal**: `modulo_4`

#### [fast-food-cook-to-order](https://github.com/fiap-software-architecture-tech/fast-food-cook-to-order)
**Microsserviço de Preparação (CTO)** - Controle da cozinha e preparação de pedidos.

- **Responsabilidade**: Gerenciamento da fila de preparação e status dos pedidos
- **Comunicação**: Eventos de mudança de status de preparação
- **Branch Principal**: `modulo_4`

### ☁️ Infraestrutura

#### [fast-food-k8s-infra](https://github.com/fiap-software-architecture-tech/fast-food-k8s-infra)
**Infraestrutura Kubernetes** - Provisionamento de cluster EKS, ECR e recursos de orquestração.

- **Tecnologias**: Terraform, AWS EKS, AWS ECR
- **Recursos**: Cluster Kubernetes, Registry de containers, Networking
- **Features**: Auto-scaling (HPA), Load Balancing, Metrics Server
- **Branch Principal**: `modulo_4`

#### [fast-food-db-infra](https://github.com/fiap-software-architecture-tech/fast-food-db-infra)
**Infraestrutura de Banco de Dados** - Provisionamento de RDS MySQL gerenciado.

- **Tecnologias**: Terraform, AWS RDS
- **Recursos**: MySQL gerenciado, Backups automáticos, High Availability
- **Branch Principal**: `modulo_4`

---

## 🎯 Funcionalidades do Sistema

### Módulos Implementados

✅ **Gerenciamento de Clientes**
- Cadastro de clientes por CPF
- Autenticação via Lambda serverless
- Identificação para fidelização

✅ **Catálogo de Produtos**
- Gerenciamento de produtos e categorias
- Controle de estoque
- Customização de pedidos

✅ **Sistema de Pedidos**
- Criação de pedidos no totem
- Acompanhamento de status em tempo real
- Fila de preparação otimizada

✅ **Processamento de Pagamentos**
- Integração com Mercado Pago
- Confirmação via webhook
- Validação de transações

✅ **Preparação na Cozinha**
- Controle de fila de preparação
- Status de pedidos (Recebido → Em Preparação → Pronto → Finalizado)
- Notificações de conclusão

---

## 🛠️ Stack Tecnológica

### Backend
- **Linguagem**: TypeScript / Node.js
- **Framework**: Fastify
- **ORM**: Prisma
- **Validação**: Zod
- **Arquitetura**: Hexagonal (Ports & Adapters)
- **Padrões**: DDD, Clean Architecture

### Infraestrutura
- **Cloud Provider**: AWS
- **Orquestração**: Kubernetes (EKS)
- **Containers**: Docker, Amazon ECR
- **Database**: Amazon RDS MySQL
- **Serverless**: AWS Lambda, API Gateway
- **IaC**: Terraform
- **CI/CD**: GitHub Actions

### Observabilidade
- **Logs**: CloudWatch Logs
- **Métricas**: Kubernetes Metrics Server
- **Monitoramento**: CloudWatch, kubectl

---

## 🚀 Deploy e Execução

### Pré-requisitos

- AWS Account com permissões adequadas
- Docker e Docker Compose
- Node.js 18+ / 22+
- Terraform >= 1.0
- kubectl
- AWS CLI configurado

### Pipeline de Deploy Automatizado

O sistema utiliza **GitHub Actions** para CI/CD completamente automatizado:

```
1. Database Infra (fast-food-db-infra)
   ↓
2. K8s Infra (fast-food-k8s-infra)
   ↓
3. Lambda Auth (fast-food-auth)
   ↓
4. Microsserviços (Order, Payment, CTO)
   ↓
5. Application Deploy
```

### Execução Local para Desenvolvimento

```bash
# 1. Clone o repositório desejado
git clone https://github.com/fiap-software-architecture-tech/fast-food.git
cd fast-food

# 2. Configure variáveis de ambiente
cp .env.example .env

# 3. Suba com Docker Compose
docker-compose up --build

# 4. Acesse a aplicação
# API: http://localhost:3000
# Swagger: http://localhost:3000/docs
```

Para instruções detalhadas de cada repositório, consulte o README específico de cada um.

---

## 📊 Gestão de Custos AWS

⚠️ **IMPORTANTE**: O projeto utiliza recursos AWS que geram custos. Para evitar cobranças desnecessárias:

### Workflows de Cleanup Disponíveis

Cada repositório possui workflows de cleanup via GitHub Actions:

- **fast-food**: `Cleanup - Application and Infrastructure`
- **fast-food-k8s-infra**: `Cleanup - Destroy Kubernetes`
- **fast-food-db-infra**: `Cleanup - Destroy Database`
- **fast-food-auth**: `Cleanup - Destroy Lambda`

### Estimativa de Custos

| Recurso | Custo Mensal Estimado |
|---------|----------------------|
| RDS MySQL (db.t3.micro) | ~$15-30 |
| EKS Cluster | ~$73 |
| Lambda Auth (pay-per-request) | ~$0-5 |
| ECR Storage | ~$1-5 |
| Data Transfer | ~$5-10 |
| **Total Estimado** | **~$94-123/mês** |

💡 **Dica**: Execute os workflows de cleanup após apresentações/testes para minimizar custos.

---

## 📹 Vídeos de Apresentação

### Fase 1 - Arquitetura Monolítica
[📹 Assistir no Google Drive](https://drive.google.com/file/d/1g7Sn-VOfrwDRkErXO3EoisZLAg4psrhD/view)

### Fase 2 - Infraestrutura como Código
[📹 Assistir no Google Drive](https://drive.google.com/file/d/1I3kuTuB8rHYfieVRkhryJwcm9AV9dKFI/view?usp=sharing)

### Fase 3 - Serverless e Escalabilidade
[📹 Assistir no Google Drive](https://drive.google.com/file/d/1BHgr36XaW9gyuWwWTdwwLPk7bCVMNAkS/view?usp=sharing)

### Fase 4 - Microsserviços (Em Desenvolvimento)
🚧 Em desenvolvimento

---

## 👥 Time de Desenvolvimento

**Grupo 277 - SOAT FIAP**

| Nome | RM | GitHub | Discord |
|------|-----|--------|---------|
| Leonardo Andreas | 361923 | [@laahundskarl](https://github.com/laahundskarl) | leooandreas |
| Gabriel Gomes | 361899 | [@gabrielgsd1](https://github.com/gabrielgsd1) | gabrielgsd |
| Willian Borba | 364043 | [@WillianBorba](https://github.com/WillianBorba) | willianrocha |
| Fabio Smaniotto | 362223 | [@fabiosb](https://github.com/fabiosb) | ofabiosb |

---

## 📖 Documentação Adicional

### Event Storming e DDD

Documentação completa de Event Storming, diagramas de domínio e decisões arquiteturais estão disponíveis na pasta `/docs` do repositório [fast-food](https://github.com/fiap-software-architecture-tech/fast-food/tree/modulo_4/docs).

### Diagramas de Arquitetura

- **Arquitetura Geral**: Disponível em cada repositório
- **Diagrama de Banco de Dados**: [fast-food/docs](https://github.com/fiap-software-architecture-tech/fast-food/tree/modulo_4/docs)
- **Fluxos de Negócio**: Event Storming na pasta docs

### APIs e Coleções

Coleções Postman para testes estão disponíveis na pasta `/api` do repositório principal.

---

## 🤝 Contribuindo

Este projeto é parte de um trabalho acadêmico da FIAP. Contribuições são feitas exclusivamente pelos membros do grupo.

### Padrões de Desenvolvimento

- **Versionamento**: Git Flow
- **Commits**: Conventional Commits
- **Código**: ESLint + Prettier
- **Testes**: Jest (onde aplicável)
- **CI/CD**: GitHub Actions

### Estrutura de Branches

- `main` / `modulo_4`: Branch principal (produção)
- `develop`: Branch de desenvolvimento
- `feature/*`: Features em desenvolvimento
- `hotfix/*`: Correções urgentes

---

## 📝 Licença

Este projeto foi desenvolvido como parte do programa de pós-graduação em Software Architecture da FIAP e é de propriedade acadêmica do **Grupo 277**.

---

## 🎓 Sobre a FIAP

A **FIAP (Faculdade de Informática e Administração Paulista)** é uma instituição de ensino superior reconhecida pela excelência em cursos de tecnologia. O programa de **Software Architecture** é um curso de pós-graduação lato sensu focado em formar profissionais capazes de projetar e implementar arquiteturas de software escaláveis, resilientes e modernas.

### Programa SOAT - Software Architecture

O curso aborda:
- Arquitetura de Software e Padrões de Projeto
- Microserviços e Arquitetura Distribuída
- Cloud Computing (AWS, Azure, GCP)
- DevOps e CI/CD
- Domain-Driven Design (DDD)
- Escalabilidade e Performance
- Segurança e Observabilidade

---

## 📞 Contato

Para questões relacionadas ao projeto, entre em contato com os membros do grupo via GitHub ou Discord.

**FIAP - Software Architecture Tech Challenge 2025/2026**
**Grupo 277**
