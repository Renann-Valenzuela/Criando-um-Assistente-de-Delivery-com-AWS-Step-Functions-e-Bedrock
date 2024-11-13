# Assistente de Delivery com AWS Step Functions e Amazon Bedrock

Este projeto visa criar um assistente de delivery automatizado usando AWS Step Functions e Amazon Bedrock. O objetivo é orquestrar diferentes serviços AWS para gerenciar um fluxo de pedidos, desde a recepção até a entrega final.

## Pré-requisitos

Antes de começar, é importante garantir que você tenha as seguintes permissões e configurações:
- **Conta AWS** com acesso ao Amazon Step Functions e Amazon Bedrock.
- Permissões para configurar e usar serviços relacionados ao AWS Lambda, SQS, SNS, etc.
- Ambiente configurado para executar funções Lambda e gerenciar os fluxos de Step Functions.

## Situação do Problema

A situação do problema é gerenciar o fluxo de pedidos de delivery, que envolve os seguintes passos:
1. Recepção do pedido.
2. Validação do pedido.
3. Integração com sistemas de pagamento.
4. Atualização do status de entrega.
5. Entrega final e feedback.

Para isso, utilizaremos o **AWS Step Functions** para orquestrar as etapas e o **Amazon Bedrock** para personalizar a interação com os usuários de maneira inteligente.

## Links de Referência

1. [Página oficial do AWS Step Functions](https://aws.amazon.com/pt/step-functions/)
2. [Exemplos do GitHub](https://github.com/aws-samples/aws-stepfunctions-examples)
3. [Como criar um assistente virtual com Amazon Bedrock](https://aws.amazon.com/pt/blogs/aws-brasil/como-criar-um-assistente-virtual-de-baixa-latencia-com-multiplos-modelos-usando-serverless-e-amazon-bedrock/)

## Workflow Studio & ASL

Para orquestrar as tarefas, vamos usar o **AWS Step Functions** com a linguagem **Amazon States Language (ASL)**. O ASL define os estados e transições do fluxo de trabalho.

# Precificação e Custos

O uso do **AWS Step Functions** e do **Amazon Bedrock** será cobrado com base no número de transições de estado e no tempo de execução. Aqui estão alguns detalhes sobre a cobrança:

- **AWS Step Functions**: A cobrança é feita pelo número de transições de estado e pelo tempo de execução de cada estado.
- **Amazon Bedrock**: A cobrança depende do uso de modelos AI, com base no número de chamadas realizadas e no tempo de execução de cada modelo.

Para mais detalhes sobre os custos, consulte as páginas de precificação:

- [Precificação do AWS Step Functions](#)
- [Precificação do Amazon Bedrock](#)

---

# Níveis de Configuração

## Nível 1: Permissões de Perfil

Certifique-se de que as funções Lambda e os serviços envolvidos no fluxo de trabalho tenham permissões adequadas para acessar os recursos da AWS necessários. As permissões devem ser configuradas no **IAM (Identity and Access Management)**.

## Nível 2: Disponibilidade de Serviço

Verifique se os serviços necessários, como o **Amazon Bedrock** e **AWS Lambda**, estão disponíveis na sua região. Nem todos os serviços podem estar disponíveis em todas as regiões, por isso é importante verificar a compatibilidade antes de começar a implementação.

---

# Criando um Assistente de Delivery na Prática

Agora vamos implementar as etapas do assistente de delivery, integrando o **Step Functions** e o **Amazon Bedrock** para personalizar a experiência do usuário.

## Exemplo de Fluxo Completo para o Assistente de Delivery

Aqui está o fluxo de trabalho que orquestra a recepção de pedidos, validação de pagamento e entrega.

```json
{
  "Comment": "Fluxo de trabalho do Assistente de Delivery",
  "StartAt": "ReceberPedido",
  "States": {
    "ReceberPedido": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:ReceberPedido",
      "Next": "ValidarPagamento"
    },
    "ValidarPagamento": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:ValidarPagamento",
      "Next": "ProcessarPedido"
    },
    "ProcessarPedido": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:ProcessarPedido",
      "Next": "AtualizarStatus"
    },
    "AtualizarStatus": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:AtualizarStatus",
      "Next": "EntregarPedido"
    },
    "EntregarPedido": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:EntregarPedido",
      "End": true
    }
  }
}
```
# Integração com Amazon Bedrock para Personalização

Você pode usar o **Amazon Bedrock** para personalizar o assistente, tornando a interação mais eficiente e personalizada.
```json
{
  "Comment": "Integrando com Amazon Bedrock",
  "StartAt": "InteragirComUsuario",
  "States": {
    "InteragirComUsuario": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:InteragirComUsuario",
      "Parameters": {
        "Model": "Claude",
        "Prompt": "Qual é o seu pedido hoje?"
      },
      "Next": "ValidarPedido"
    },
    "ValidarPedido": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:ValidarPedido",
      "Next": "ProcessarPagamento"
    },
    "ProcessarPagamento": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:REGION:ACCOUNT_ID:function:ProcessarPagamento",
      "Next": "FinalizarPedido"
    },
    "FinalizarPedido": {
      "Type": "Pass",
      "Result": "Pedido Finalizado com Sucesso!",
      "End": true
    }
  }
}
```
### Conclusão
Este projeto de Assistente de Delivery usando AWS Step Functions e Amazon Bedrock permite criar uma experiência de delivery automatizada e personalizada, com orquestração de tarefas e interações inteligentes. Certifique-se de seguir as orientações acima para configurar corretamente seu fluxo de trabalho, integrar os serviços AWS necessários e otimizar o assistente de acordo com as preferências dos usuários.

### Referências:
AWS Step Functions - Documentação Oficial
Exemplos de Step Functions no GitHub
Criando um Assistente Virtual com Amazon Bedrock
