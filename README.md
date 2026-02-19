Lead Flow — Official API Orchestration

Sistema de orquestração de leads com envio via API Oficial do WhatsApp e fluxo automatizado de retrabalho D+3.

Integra Webhooks em Node.js, API REST da Extensão Chrome, Chatwoot e PostgreSQL para garantir rastreabilidade completa da operação comercial.

📌 Visão Geral da Arquitetura

Extensão Chrome (API REST)
→ Webhook Node.js
→ Tratamento e validação de dados
→ Integração com Chatwoot
→ Persistência em PostgreSQL
→ Disparo via API Oficial WhatsApp

🔹 FLUXO 1 — API OFICIAL

Fluxo principal responsável por registrar, atribuir e enviar mensagem oficial ao lead indicado pelo consultor.

🎯 Objetivo

Garantir que todo lead indicado:

Seja registrado no banco

Seja atribuído corretamente

Receba mensagem oficial padronizada

Tenha rastreabilidade completa

🧩 Origem

Extensão personalizada do Google Chrome utilizada na tela de ligação.

A extensão realiza chamada via API REST para o backend Node.js enviando:

Nome

Telefone

CNPJ

Consultor responsável

Status de indicação

⚙ Processamento no Backend (Node.js)

Recebe requisição via Webhook

Normaliza dados (JSON parsing)

Valida campos obrigatórios

Verifica existência do contato no Chatwoot

📌 Cenário A — Contato não existe

Cria contato no Chatwoot

Cria conversa

Registra mensagem inicial

Persiste lead no PostgreSQL

Atribui conversa ao consultor

Envia template via API Oficial (botão interativo 24h)

📌 Cenário B — Contato já existe

Reatribui conversa ao consultor

Atualiza registro no banco

Envia mensagem oficial

🗄 Persistência

Cada lead recebe:

Identificador único

Origem (API Oficial)

Data de criação

Status operacional

Controle de retrabalho

🔁 FLUXO 2 — RETRABALHO API OFICIAL (D+3)

Fluxo automatizado responsável por reprocessar leads não convertidos.

Executado diariamente às 09:00.

🎯 Objetivo

Evitar estagnação de oportunidades comerciais.

Garantir segundo contato estruturado após 3 dias.

⚙ Processamento

Consulta PostgreSQL buscando leads com 3 dias

Filtra leads qualificados e não convertidos

Verifica existência no Chatwoot

Reprocessa envio

📌 Caso contato não exista

Cria contato

Cria nova conversa

Envia nova mensagem oficial

Marca como retrabalho_api_oficial

📌 Caso contato já exista

Cria nova conversa

Envia novo template

Atualiza status no banco

🏗 Stack Tecnológica

Backend:

Node.js

Express (API REST)

Webhooks estruturados

Extensão:

Google Chrome Extension

Comunicação via API REST

Banco de Dados:

PostgreSQL

Mensageria:

API Oficial WhatsApp (Meta)

Gestão de Conversas:

Chatwoot

Manipulação de Dados:

JSON estruturado

Validações e normalização de payload

🔐 Governança e Controle

O sistema garante:

Registro completo de cada lead

Separação clara entre fluxo principal e retrabalho

Histórico de interações

Controle por consultor

Rastreabilidade de envio oficial

📈 Benefícios Operacionais

Redução de perda de leads

Automatização do follow-up

Padronização institucional

Maior controle gerencial

Arquitetura preparada para escalar
