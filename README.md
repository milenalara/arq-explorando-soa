# Serviços - Arquitetura SOA

## 1. Serviço de Investimento

**Objetivo:**  
Permitir a compra e venda de ativos financeiros, como CDBs, oferecendo serviço de corretagem.

**Quem consome:**  
App mobile, plataforma web.

**Quais dados ou sistemas acessa:**  
Sistema de registro de ativos, base de ativos disponíveis, dados de saldo e perfil do cliente.

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
App mobile, parceiros fintechs, módulo de empréstimo.

**Quais dados ou sistemas acessa:**  
Score externo (Serasa/Boa Vista), histórico de transações, cadastro do cliente.

---

## 4. Serviço de Notificações

**Objetivo:**  
Enviar alertas e confirmações ao cliente sobre eventos financeiros (compra no cartão, saque, etc).

**Quem consome:**  
Serviço de pagamento com cartão, serviço de saque, app mobile.

**Quais dados ou sistemas acessa:**  
Sistema de eventos, push notifications, email/SMS.
