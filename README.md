# 🚀 Automação de Notificação de Novos Clientes com n8n + SQL Server

![Workflow Status](https://img.shields.io/badge/automação-ativa-brightgreen)
![SQL Server](https://img.shields.io/badge/banco-SQL--Server-4479A1)
![n8n](https://img.shields.io/badge/n8n-automação-orange)

Este projeto automatiza o envio de e-mails de boas-vindas para novos clientes cadastrados em uma tabela SQL Server, usando a plataforma **n8n**. O sistema envia automaticamente um e-mail para cada novo cliente e marca o status de envio no banco de dados.

---

## 🧩 Tecnologias Utilizadas

- [n8n](https://n8n.io) – Plataforma de automação de workflows
- Microsoft SQL Server – Banco de dados relacional
- SMTP (via Mailtrap) – Envio de e-mails em ambiente de teste
- [Mailtrap](https://mailtrap.io) – Captura e visualização segura de e-mails durante o desenvolvimento

---

## 📂 Estrutura da Tabela `Clientesn8n`

```sql
CREATE TABLE Clientesn8n (
  Id INT IDENTITY(1,1) PRIMARY KEY,
  Nome NVARCHAR(200) NOT NULL,
  Email NVARCHAR(200) NOT NULL,
  DataRegistro DATETIME DEFAULT GETDATE(),
  EnviadoEmail BIT DEFAULT 0,
  rowverssion TIMESTAMP
);
