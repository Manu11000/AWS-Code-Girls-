# 🧠 Desafio 02 — Automação de Workflows com AWS Step Functions


##  Objetivo

Desenvolver e compreender como **Step Functions** podem orquestrar diferentes serviços da AWS para criar fluxos automatizados, seguros e observáveis.


## 🏗️ Conceito

O **AWS Step Functions** permite criar fluxos visuais de execução, onde cada etapa é representada por um **estado**.  
Esses estados podem:
- Executar funções Lambda;
- Esperar por eventos;
- Fazer ramificações condicionais;
- Repetir execuções ou capturar erros.

---

## 🔧 Caso de uso (ligado ao projeto anterior)

Neste contexto, imagine que:
- Quando um **usuário faz upload de um novo cenário RPG no S3**, uma **função Lambda** é acionada.
- Essa Lambda inicia uma **Step Function** que:
  1. Processa o arquivo (validação e redimensionamento);
  2. Atualiza um banco de dados ou metadado;
  3. Envia uma notificação de conclusão (por e-mail ou SNS).

Assim, o fluxo de trabalho fica automatizado e rastreável.

---

## 📚 Recursos utilizados
- **AWS Step Functions**
- **AWS Lambda**
- **Amazon S3**
- **IAM Roles**
- **DynamoDB**

---

📅 **Bootcamp Santander Code Girls — AWS & Cloud Computing**

---

