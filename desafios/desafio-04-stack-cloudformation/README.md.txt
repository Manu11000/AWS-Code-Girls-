# 🧱 Desafio 04 — Criação de Stacks com AWS CloudFormation

Implementar a **primeira Stack** utilizando o **AWS CloudFormation**, explorando o conceito de **Infraestrutura como Código (IaC)** dentro do mesmo caso de uso — a aplicação de criação e processamento de cenários de RPG.

---

## 🎯 Objetivo

Compreender como o **AWS CloudFormation** permite **automatizar a criação e gerenciamento de recursos AWS**, garantindo padronização, rastreabilidade e facilidade de replicação do ambiente.

---

## 🏗️ Caso de uso: Stack para o sistema RPG

Nesta stack, os recursos do projeto anterior são definidos de forma automatizada, permitindo que todo o ambiente seja criado com apenas um arquivo (`.yaml` ou `.json`).

### Recursos simulados:

1. **Amazon EC2** — instância principal do sistema RPG;  
2. **Amazon EBS** — volume de armazenamento persistente conectado à EC2;  
3. **Amazon S3** — bucket para armazenamento de imagens e mapas;  
4. **AWS Lambda** — função para processar uploads;  
5. **AWS Step Functions** — orquestração e validação dos workflows.

---

## 🔧 Estrutura geral do template:

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: "Stack do Sistema RPG - Bootcamp Santander Code Girls"

Resources:
  RPGS3Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: "rpg-cenarios-upload"

  RPGLambdaFunction:
    Type: AWS::Lambda::Function
    Properties:
      Handler: index.handler
      Runtime: python3.9
      Role: arn:aws:iam::123456789012:role/LambdaBasicExecution
      Code:
        ZipFile: |
          def handler(event, context):
              print("Processando cenário RPG...")

  RPGInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0abcdef1234567890
      InstanceType: t2.micro
      KeyName: rpg-keypair
