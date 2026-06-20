# Human in the Loop com IA, Redis e Telegram (n8n)

## Visão Geral

Este projeto demonstra a implementação de um fluxo **Human in the Loop** utilizando **n8n**, **Google Gemini**, **Redis** e **Telegram**.

O objetivo é garantir que todo conteúdo gerado por Inteligência Artificial passe por validação humana antes de ser considerado aprovado.

Além disso, o projeto implementa um mecanismo de fila de mensagens utilizando Redis para agrupar mensagens enviadas em sequência, evitando execuções desnecessárias da IA, reduzindo custos operacionais e melhorando a experiência do usuário.

Os conteúdos aprovados são armazenados em uma **Data Table do n8n**, permitindo persistência e rastreabilidade das aprovações realizadas.

---

## Principais Recursos

- Integração com Telegram
- Human in the Loop
- Aprovação humana obrigatória
- Revisão automática baseada em feedback
- Fila de mensagens com Redis
- Agrupamento de mensagens em buffer
- Pesquisa web com Tavily Search
- Integração com Google Gemini
- Persistência de dados utilizando Data Tables do n8n
- Arquitetura modular utilizando sub-workflows
- Redução de custos com IA através de consolidação de mensagens

---

## Arquitetura

```text
Usuário (Telegram)
        │
        ▼
Fila de Mensagens (Redis)
        │
        ▼
Agente de IA (Gemini)
        │
        ▼
Aprovação Humana
        │
        ▼
      Aprovado?
     ┌────┴────┐
     │         │
    Sim       Não
     │         │
     ▼         ▼
Armazena    Revisa Conteúdo
no Banco         │
     │           │
     └─────┬─────┘
           ▼
      Resultado Final
```

---

##  Workflows

### Human In the Loop

Workflow principal responsável por:

- Receber mensagens do Telegram
- Acionar o sub-workflow de fila
- Gerar conteúdo utilizando IA
- Realizar pesquisas complementares com Tavily
- Solicitar aprovação humana
- Classificar automaticamente o feedback recebido
- Regerar o conteúdo quando houver solicitações de alteração
- Armazenar conteúdos aprovados em Data Tables do n8n

### Fila de Mensagens (Sub-workflow)

Workflow auxiliar responsável por:

- Agrupar mensagens enviadas em sequência
- Armazenar mensagens temporariamente no Redis
- Aguardar novas entradas durante uma janela de tempo
- Consolidar mensagens fragmentadas
- Evitar múltiplas execuções da IA para uma mesma solicitação

---

## Tecnologias Utilizadas

- n8n
- Google Gemini
- Telegram Bot API
- Redis
- Tavily Search
- Data Tables (n8n)

---

##  Objetivo do Projeto

Demonstrar padrões avançados de automação utilizando n8n, incluindo:

- Human in the Loop
- Orquestração de Agentes de IA
- Filas de Mensagens
- Persistência de Dados
- Processamento Assíncrono
- Integração com APIs Externas
- Workflows Modulares

---

## 📂 Estrutura do Repositório

```text
.

│── Human In the Loop.json
│── Fila de MSG Sub-workflow.json
│
├
│
└── README.md
```

---

## ⚙️ Como Utilizar

### Pré-requisitos

- n8n
- Redis
- Bot do Telegram
- Chave da API Google Gemini
- Chave da API Tavily

### Instalação

1. Importe os dois workflows no n8n.
2. Configure as credenciais do Telegram.
3. Configure as credenciais do Google Gemini.
4. Configure as credenciais do Redis.
5. Configure as credenciais do Tavily Search.
6. Ative os workflows.
7. Envie uma mensagem para o bot no Telegram.

---

##  Caso de Uso

O usuário envia uma solicitação pelo Telegram.

Caso envie várias mensagens seguidas, o sistema as agrupa utilizando Redis antes de processar.

Após consolidar a solicitação, um agente de IA gera o conteúdo e o envia para aprovação humana.

O usuário pode:

- Aprovar o conteúdo
- Solicitar ajustes
- Solicitar reescritas

Enquanto houver solicitações de alteração, o fluxo continua iterando entre IA e usuário.

Quando aprovado, o conteúdo é armazenado automaticamente em uma Data Table do n8n.

---

## Conceitos Demonstrados

Este projeto foi desenvolvido com foco em demonstrar conhecimentos práticos em:

- Automação de Processos
- Engenharia de Prompts
- IA Generativa
- Human in the Loop
- Redis
- Filas e Buffers de Mensagens
- Persistência de Dados
- Arquitetura de Workflows
- Integração entre Múltiplos Serviços
- Desenvolvimento de Soluções com n8n

---

## 📄 Licença

Este projeto está disponível para fins educacionais, demonstração técnica e portfólio profissional.
