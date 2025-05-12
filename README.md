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


🔁 Funcionamento do Workflow no n8n
Etapas do processo:
⏰ Schedule Trigger

Executa a cada 10 segundos para verificar novos registros.

🗃️ Consulta SQL

Seleciona clientes com EnviadoEmail = 0 ou NULL.

🔎 Condição (If)

Verifica se existem registros a serem processados.

📧 Envio de E-mail

Dispara um e-mail HTML personalizado para cada cliente.

✅ Atualização no Banco

Atualiza o campo EnviadoEmail para 1, evitando reenvios.

💌 Exemplo de E-mail Enviado
html
Copy
Edit
<html>
  <body>
    <h2>Olá, {{ $json.Nome }}!</h2>
    <p>Seja bem-vindo à nossa plataforma.</p>
    <p>Estamos felizes em ter você conosco.</p>
    <p>Se precisar de ajuda, é só responder este e-mail.</p>
    <br>
    <p>Atenciosamente,<br>Sua equipe.</p>
  </body>
</html>
🧪 Ambiente de Teste com Mailtrap
O envio de e-mails foi testado com a ferramenta Mailtrap, que simula a entrega real de e-mails em ambiente seguro para desenvolvimento.

🔗 Mensagem de teste disponível em:
https://mailtrap.io/inboxes/3691548/messages/4875964889
