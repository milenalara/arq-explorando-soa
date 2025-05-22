# Serviços - Arquitetura SOA

# 3. Processo de Saque de Dinheiro

## Objetivo
Permitir que o cliente realize o saque de valores de sua conta para dinheiro físico ou transferência para outra conta, com validações automáticas de saldo e comunicação com sistemas financeiros e de autenticação.

## Quem consome
- App mobile
- APIs de parceiros (ex: caixas eletrônicos, fintechs)

## Serviços utilizados e justificativas

### 1. Autenticação de Cliente
- **Justificativa:** Confirma a identidade do cliente antes de autorizar a operação de saque, garantindo segurança.
- **Características:** Serviço reutilizado por diversos processos (pagamentos, transferências, investimentos). Autônomo e executável via API, com granularidade baixa.

### 2. Validação de Saldo
- **Justificativa:** Verifica se o cliente possui saldo suficiente para efetuar o saque.
- **Características:** Serviço técnico, pontual e reutilizável em processos como pagamentos, investimentos e transferências.

### 3. Registro de Operação de Saque
- **Justificativa:** Formaliza a operação no sistema financeiro e contabiliza a saída de recursos.
- **Características:** Serviço SOA clássico, executável automaticamente, com escopo técnico bem definido. Pode ser implementado via REST ou SOAP.

### 4. Atualização de Saldo
- **Justificativa:** Atualiza o saldo do cliente após a realização do saque, mantendo a consistência das informações financeiras.
- **Características:** Serviço altamente reutilizável por diversos processos (pagamentos, investimentos, etc).

### 5. Notificações
- **Justificativa:** Envia aviso ao cliente confirmando o sucesso do saque.
- **Características:** Serviço compartilhado com vários outros processos (pagamentos, crédito, investimentos). Integra-se a múltiplos canais: push, email, SMS.

## Dados ou sistemas acessados
- Banco de dados transacional (saldo, limite disponível)
- Sistema de autenticação
- Sistema de registro de operações financeiras
- Sistema de notificações

## Explicação

| **Critério**       | **Aplicação no Processo de Saque**                                                                 |
|--------------------|---------------------------------------------------------------------------------------------------|
| **Escopo**         | Macroscópico – abrange autenticação, validação, execução e notificação.                            |
| **Granularidade**  | Alta – representa um processo completo de negócio.                                                 |
| **Reutilização**   | Baixa no processo (específico para saque), alta nos serviços utilizados (compartilhados).          |
| **Composição**     | Composto por tarefas técnicas e decisões de negócio.                                               |
| **Tecnologia**     | Independente – pode ser descrito em BPMN ou implementado com diferentes padrões (REST, SOAP, etc). |
| **Interface**      | Pode ser modelado em BPMN, consumido via app, APIs externas (ex: fintechs, caixas eletrônicos).     |
| **Autonomia Técnica** | Baixa – depende da orquestração de múltiplos serviços para sua execução.                        |

![alt text](image.png)
---
