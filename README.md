# Fluxo Linear com AWS Step Functions

##  Objetivo do Projeto

Este projeto demonstra a **estrutura básica** de um workflow no AWS Step Functions, focando na **sequência linear** de estados e na **passagem de dados** usando o **Estado `Pass`**. É uma consolidação do uso da sintaxe da **Amazon States Language (ASL)**.

## Tecnologias e Conceitos Aplicados

| Serviço AWS | Função no Workflow | Insights Chave |
| :--- | :--- | :--- |
| **AWS Step Functions** | Orquestrador principal. | **Sequência de Estados (`Next`)**. |
| **Estado `Pass`** | Simula processamento e injeta metadados. | Demonstra a manipulação básica de dados em ASL. |
| **Estado `Succeed`** | Encerra o fluxo com sucesso. | Demonstra a forma padrão de conclusão. |

## 1. Definição da Máquina de Estados 

O fluxo segue uma linha reta: Iniciar -> Processar -> Finalizar.

```json

{
  "Comment": "A estrutura: Iniciar, Passar Dados, Finalizar.",
  "StartAt": "InicializarDados",
  "States": {
    "InicializarDados": {
      "Type": "Pass",
      "Comment": "Simula o recebimento ou criação de um dado inicial.",
      "Result": {
        "status": "Iniciado",
        "versao": "1.0"
      },
      "ResultPath": "$.meta", 
      "Next": "ProcessarPasso"
    },
    "ProcessarPasso": {
      "Type": "Pass",
      "Comment": "Simplesmente passa o input adiante, simulando um processamento.",
      "Next": "FinalizarSucesso"
    },
    "FinalizarSucesso": {
      "Type": "Succeed"
    }
  }
}
