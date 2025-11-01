# ✅ Desafio 03 — Validação de Workflows com AWS Step Functions

Consolidação do entendimento sobre **validação e controle de fluxos automatizados** dentro do **AWS Step Functions**, mantendo o mesmo caso de uso prático: O Sistema de Criação de Cenários para RPG.

---

## 🎯 Objetivo

Explorar como o **Step Functions** pode validar o sucesso ou falha de cada etapa do workflow, garantindo que processos automatizados (como upload e processamento de cenários) sejam executados com controle e tratamento de erros.

---

## 🧩 Caso de uso: Validação do fluxo de processamento RPG

Fluxo geral:

1. O usuário realiza upload de um **novo cenário** no **S3**.
2. Um **evento S3** dispara uma **função Lambda** responsável por iniciar a **Step Function**.
3. A **Step Function**:
   - Processa o arquivo (validação de formato e tamanho);
   - Redimensiona imagens (caso aplicável);
   - Valida se o processamento ocorreu corretamente;
   - Envia notificações dependendo do resultado.

---

## 🔄 Diagrama lógico do fluxo

```text
Start
  ↓
Lambda (Validar Upload)
  ↓
Choice (Upload válido?)
   ├── Sim → Processar Arquivo → Validar Resultado → Notificar Sucesso → End (Succeed)
   └── Não → Notificar Erro → End (Fail)
