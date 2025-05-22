# Serviços - Arquitetura SOA

## 1. Processo de Investimento em Títulos com Juros Pré-Fixados

### 1.1. Objetivo
Permitir que o cliente realize a compra de títulos com rendimento pré-fixado, garantindo validações automáticas e comunicação com o sistema de registro de ativos.

### 1.2. Quem consome
App mobile e plataforma web.

### 1.3. Serviços utilizados e justificativas

#### 1.3.1. Consulta de Ativos Pré-Fixados

Filtra e exibe apenas os títulos com taxa de juros conhecida no momento da compra. Reutilizável em processos de recomendação e simulações financeiras. Executável via REST API, com granularidade baixa e alta autonomia.

#### 1.3.2. Validação de Perfil do Cliente
Verifica se o perfil de investidor do cliente (ex: conservador, moderado) é compatível com o ativo. Reutilizável em outros processos como recomendação de carteira e onboarding. Serviço técnico com decisão pontual.

#### 1.3.3. Validação de Saldo
Confirma se o cliente possui saldo suficiente. Serviço reutilizável em transações financeiras diversas. Executável automaticamente via API, granularidade baixa.

#### 1.3.4. Registro da Ordem de Compra
Formaliza a compra com o sistema de custódia de ativos. Serviço técnico clássico de SOA, interoperável, com escopo bem definido.

#### 1.3.5. Atualização de Saldo
Deduz valor da compra do saldo do cliente. Reutilizável em vários processos (pagamento, saque, crédito). Executável via REST.

#### 1.3.6. Notificações
Informa o cliente sobre a conclusão da compra. Reutilizável em diversas operações. Pode ser disparado por push, e-mail ou SMS.

### 1.4. Dados ou sistemas acessados:

- Sistema de registro de ativos
- Base de dados de ativos disponíveis (filtrados por tipo pré-fixado)
- Dados de saldo e perfil do cliente

## 2. Processo de Investimento em Títulos com Juros Pós-Fixados

### 2.1. Objetivo
Permitir que o cliente invista em ativos com rendimento atrelado a um indicador variável (ex: CDI), com validações específicas e comunicação com sistema de registro de ativos.

### 2.3. Quem consome
App mobile e plataforma web.

### 2.4. Serviços utilizados e justificativas

#### 2.4.1. Consulta de Ativos Pós-Fixados
Lista apenas os ativos vinculados a taxas variáveis. Utilizável também por sistemas de simulação de rendimento ou alertas de variação. Executável por API com granularidade baixa.

#### 2.4.2 Validação de Perfil do Cliente
Verifica se o cliente está apto a investir em produtos de renda variável ou indexados. Técnica pontual, reutilizável em outros fluxos.

#### 2.4.3 Validação de Saldo
Confere disponibilidade de saldo. Reutilizável. Executável de forma autônoma.

#### 2.4.4. Registro da Ordem de Compra
Formaliza a operação com sistema de registro de ativos. Interoperável e independente de plataforma (ex: REST, SOAP).

#### 2.4.5. Atualização de Saldo
Atualiza o saldo do cliente após o investimento. Usado em vários fluxos.

#### 2.4.6. Notificações
Informa o sucesso da operação. Reutilizável. Integra com múltiplos canais.

#### 2.5. Dados ou sistemas acessados
- Sistema de registro de ativos
-  Base de dados de ativos disponíveis (filtrados por tipo pós-fixado)
- Dados de saldo e perfil do cliente

# 3. Processo de Saque de Dinheiro

## 3.1. Objetivo
Permitir que o cliente realize o saque de valores de sua conta para dinheiro físico ou transferência para outra conta, com validações automáticas de saldo e comunicação com sistemas financeiros e de autenticação.

## 3.2. Quem consome
- App mobile
- APIs de parceiros (ex: caixas eletrônicos, fintechs)

## 3.3. Serviços utilizados e justificativas

### 3.3.1. Autenticação de Cliente
- **Justificativa:** Confirma a identidade do cliente antes de autorizar a operação de saque, garantindo segurança.
- **Características:** Serviço reutilizado por diversos processos (pagamentos, transferências, investimentos). Autônomo e executável via API, com granularidade baixa.

### 3.3.2. Validação de Saldo
- **Justificativa:** Verifica se o cliente possui saldo suficiente para efetuar o saque.
- **Características:** Serviço técnico, pontual e reutilizável em processos como pagamentos, investimentos e transferências.

### 3.3.3. Registro de Operação de Saque
- **Justificativa:** Formaliza a operação no sistema financeiro e contabiliza a saída de recursos.
- **Características:** Serviço SOA clássico, executável automaticamente, com escopo técnico bem definido. Pode ser implementado via REST ou SOAP.

### 3.3.4. Atualização de Saldo
- **Justificativa:** Atualiza o saldo do cliente após a realização do saque, mantendo a consistência das informações financeiras.
- **Características:** Serviço altamente reutilizável por diversos processos (pagamentos, investimentos, etc).

### 3.3.5. Notificações
- **Justificativa:** Envia aviso ao cliente confirmando o sucesso do saque.
- **Características:** Serviço compartilhado com vários outros processos (pagamentos, crédito, investimentos). Integra-se a múltiplos canais: push, email, SMS.

## 3.4. Dados ou sistemas acessados
- Banco de dados transacional (saldo, limite disponível)
- Sistema de autenticação
- Sistema de registro de operações financeiras
- Sistema de notificações

## 3.5 Explicação

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
