# ⚙️ Desafio 06 — S3 e  Lambda

O objetivo é **consolidar conhecimentos em tarefas automatizadas com AWS Lambda e S3**, integrando o **DynamoDB** para persistência e o **LocalStack** como ambiente de testes local.

O foco é desenvolver um fluxo automatizado que simula a **execução real de uma infraestrutura AWS**, mas rodando **inteiramente em ambiente local**.

---

## 🎯 Objetivo

- Simular a AWS localmente usando **LocalStack**;
- Automatizar o processamento de arquivos enviados ao **S3**;
- Registrar as informações processadas em uma tabela **DynamoDB**;
- Compreender como esses componentes interagem em fluxos **serverless**.

---

## 🧩 Caso de uso: Sistema de Cenários RPG

A empresa voltada a 
 criação de cenários RPG deseja processar automaticamente **novos arquivos de cenário** (imagens, JSON, mapas etc.).  
Cada vez que um novo arquivo é enviado ao **S3**, uma **função Lambda** é acionada para:

1. Ler os metadados do arquivo;
2. Processar o conteúdo (por exemplo: redimensionar imagem, validar dados);
3. Registrar o resultado do processamento em uma **tabela DynamoDB**;
4. Exibir logs e confirmações no console.

---

## 🏗️ Fluxo Arquitetural

Usuário → Upload no S3 Bucket
↓
Evento S3 Trigger (Lambda)
↓
Função Lambda processa arquivo
↓
DynamoDB recebe registro do cenário
↓
 Log no CloudWatch / Local


---

## 🧱 Componentes

| Serviço | Função |
|----------|--------|
| **Amazon S3** | Armazena os arquivos de entrada (imagens, JSONs etc.) |
| **AWS Lambda** | Processa os arquivos automaticamente após upload |
| **Amazon DynamoDB** | Registra metadados e status de processamento |
| **LocalStack** | Simula localmente os serviços AWS para desenvolvimento e teste |

---

## 💻 Exemplo prático de implementação

### Estrutura do código Lambda (exemplo `lambda_function.py`)

```python
import json
import boto3

dynamodb = boto3.resource('dynamodb', endpoint_url="http://localhost:4566")
table = dynamodb.Table('cenarios_rpg')

def lambda_handler(event, context):
    print("Evento recebido:", event)
    
    for record in event['Records']:
        s3_info = record['s3']
        bucket = s3_info['bucket']['name']
        key = s3_info['object']['key']

        # Simulação de processamento
        status = "Processado com sucesso"
        
        # Registro no DynamoDB
        table.put_item(Item={
            'arquivo': key,
            'bucket': bucket,
            'status': status
        })
    
    return {'statusCode': 200, 'body': json.dumps('Processamento concluído')}


