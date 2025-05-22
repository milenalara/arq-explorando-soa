# Serviços - Arquitetura SOA

## 1. Serviço de Investimento

**Objetivo:**  
Permitir a compra e venda de ativos financeiros, como CDBs, oferecendo serviço de corretagem.

**Quem consome:**  
App mobile, plataforma web.

**Quais dados ou sistemas acessa:**  
Sistema de registro de ativos, base de ativos disponíveis, dados de saldo e perfil do cliente.

![image](https://github.com/user-attachments/assets/c2c0e5a5-3239-4598-94a3-24fb47ad9767)

Consumido por: App Mobile, Plataforma Web

Acessa: Registro de ativos, base ativos financeiros, saldo e dados do cliente

Objetivo: Negociar ativos(CDB, FIIs etc)

---

## 2. Serviço de Controle de Saldo

**Objetivo:**  
Consultar e atualizar o saldo da conta do cliente em tempo real.

**Quem consome:**  
App mobile, APIs de parceiros, módulo de extrato, serviço de saque, serviço de investimento.

**Quais dados ou sistemas acessa:**  
Banco de dados transacional, sistema contábil.

---

## 3. Serviço de Análise de Crédito

**Objetivo:**  
Avaliar o perfil de risco do cliente com base em dados financeiros e de comportamento.

**Quem consome:**  
App mobile, Web e módulo de empréstimo.

**Quais dados ou sistemas acessa:**  
Score externo (Serasa/Boa Vista), histórico de transações, cadastro do cliente.

![image](https://github.com/user-attachments/assets/13b01791-a9ec-4fe7-81f0-5ee487bc657c)

Consumido por: App/Web, módulo de empréstimos

Acessa: Score externo, histórico de gastos, dados cadastrais

Objetivo: Avaliar perfil de risco do cliente


---

## 4. Serviço de Notificações

**Objetivo:**  
Enviar alertas e confirmações ao cliente sobre eventos financeiros (compra no cartão, saque, etc).

**Quem consome:**  
Serviço de pagamento com cartão, serviço de saque, app mobile.

**Quais dados ou sistemas acessa:**  
Sistema de eventos, push notifications, email/SMS.

![image](https://github.com/user-attachments/assets/b3be652b-976a-4a64-a639-8842e1752fde)


Consumido por: Qualquer serviço que gere evento (ex: saque, compra, investimento)

Acessa: Sistemas de envio de mensagens (push/email/SMS)

Objetivo: Enviar alertas e confirmações para o cliente


---

# Processo de Saque de Dinheiro

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

---
