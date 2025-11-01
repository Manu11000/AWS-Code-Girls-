# ☁️ Desafio 05 — CloudFormation vs Terraform: Benefícios e Diferenças

O projeto tem como objetivo **implementar uma infraestrutura automatizada com AWS CloudFormation** e compreender suas **diferenças e vantagens em relação ao Terraform**, ampliando o entendimento sobre ferramentas de **Infraestrutura como Código (IaC)**.

---

## 🎯 Objetivo

- Consolidar o uso do **CloudFormation**;
- Compreender como ele se compara ao **Terraform**, em termos de arquitetura, uso e flexibilidade;
- Destacar os **benefícios, limitações e cenários de uso** de cada ferramenta.

---

## 🧩 Caso de uso: Sistema de Cenários RPG

O desafio consiste em modelar a infraestrutura do sistema  com CloudFormation, e refletir sobre como seria o mesmo ambiente usando Terraform.

Infraestrutura do sistema:
- EC2 para hospedar o servidor principal;
- EBS para armazenamento persistente;
- S3 para guardar imagens e mapas;
- Lambda + Step Functions para automação;
- (Opcional) SNS para notificações.

---

## ⚙️ CloudFormation vs Terraform

| Categoria | **CloudFormation (AWS)** | **Terraform (HashiCorp)** |
|------------|--------------------------|-----------------------------|
| **Provedor** | Nativo da AWS | Multi-cloud (AWS, Azure, GCP, etc.) |
| **Linguagem** | YAML / JSON | HCL (HashiCorp Configuration Language) |
| **Gerenciamento de Estado** | Automático dentro da AWS | Manual ou remoto via Terraform Cloud/S3 |
| **Modularidade** | Suporte via *nested stacks* | Suporte via *modules* (muito mais flexível) |
| **Velocidade de provisionamento** | Um pouco mais lenta | Mais rápida e paralelizada |
| **Rollback automático** | Sim, em caso de erro | Parcial (depende do controle de estado) |
| **Integração CI/CD** | Direta com AWS CodePipeline | Flexível, funciona com qualquer ferramenta |
| **Escopo de uso** | Focado em AWS | Multi-cloud e híbrido |

---

## 💬 Exemplo prático

- Com **CloudFormation**, podemos definir os recursos AWS diretamente em YAML e executa via console, CLI ou API.
- Com **Terraform**, podemos usar um único código `.tf` para criar a mesma infraestrutura na AWS — ou até replicá-la em outro provedor.

---

## 🧠 Benefícios do uso do CloudFormation
- Simples integração com IAM, CloudWatch e outros serviços AWS;  
- Controle de versão nativo e histórico de stacks;  
- Rollback automático em caso de falha;  
- Sem necessidade de gerenciar estado manualmente.

---

## 🌍 Benefícios do uso do Terraform
- Suporte multi-cloud (AWS, Azure, GCP, OCI etc.);  
- Reutilização de módulos;  
- Melhor controle de dependências e recursos externos;  
- Comunidade ativa e grande número de provedores customizados.

---

## 💡 Quando escolher cada um?

| Cenário | Recomendado |
|----------|--------------|
| Projeto 100% AWS | ✅ CloudFormation |
| Ambiente híbrido ou multi-cloud | ✅ Terraform |
| Time pequeno e integração com AWS CodePipeline | ✅ CloudFormation |
| Time de DevOps multi-provedores | ✅ Terraform |
