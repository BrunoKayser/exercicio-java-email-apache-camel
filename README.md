# 🛠️ Exercício de Apache Camel + Spring Boot + JavaMailSender
## 🎯 Objetivo
Neste exercício criado para auxiliar colegas de trabalho a aprender a tecnologia Apacha Camel, você irá construir uma aplicação simples utilizando **Apache Camel**, **Spring Boot** e o **JavaMailSender** para envio de e-mails.
O foco principal é praticar a criação de rotas e processadores no Apache Camel, integração entre tecnologias e uso de beans para orquestração de serviços.

---

## 📝 Enunciado
Desenvolva uma aplicação Spring Boot (Java 11 ou versão superior que seja LTS) que disponibilize um **endpoint HTTP POST** que receba uma requisição para envio de e-mail.

O fluxo deve ser gerenciado inteiramente através de uma **rota Camel**, com a utilização de **bean** para chamar o envio de e-mail via **repository**.
A validação dos dados recebidos deve ser feita utilizando um **Processor**.

---

## 🚀 Requisitos Funcionais
1. Criar um endpoint REST:
  - Rota: `/v1/api/email/send`
  - Método: `POST`
  - Consumo: `application/json`

2. O JSON de entrada deve conter os seguintes campos obrigatórios:
  - `to` (String): Endereço de e-mail do destinatário.
  - `subject` (String): Assunto do e-mail.
  - `body` (String): Conteúdo do e-mail.

3. Todos os campos devem ser **validados** em um **Processor** da rota Camel:
  - `to`:
    - Não pode ser vazio.
    - Deve ser um e-mail válido (regex simples para validar formato).
    - Não pode conter caracteres maliciosos (ex: scripts ou comandos).
  - `subject`:
    - Não pode ser vazio.
    - Deve ser verificado contra caracteres maliciosos.
  - `body`:
    - Não pode ser vazio.
    - Deve ser verificado contra caracteres maliciosos.

4. Se qualquer campo for inválido:
  - A aplicação deve retornar **HTTP 400 Bad Request** com uma mensagem explicativa sobre o erro.

5. Se todos os campos forem válidos:
  - A rota Camel deverá, via **bean**, invocar um método de um **repository** que será responsável por enviar o e-mail usando **JavaMailSender**.
  - Retornar HTTP **200 OK** com uma mensagem de sucesso.

---

## 📦 Estrutura Esperada

- **Controller**: Para receber a requisição e enviar para a rota Camel.
- **Camel Route**: Para processar a requisição, validar os dados e chamar o bean do repository.
- **Processor**: Para validar o payload.
- **Repository**: Para gerenciar o envio de e-mails usando JavaMailSender.

## 📋 Exemplo de Request
**Endpoint**:

POST http://localhost:8080/v1/api/email/send

Payload:

```json
{
  "to": "destinatario@exemplo.com",
  "subject": "Teste de envio",
  "body": "Este é um e-mail de teste enviado pela aplicação."
}
```

---

## ✅ Critérios de Aceite
- A aplicação deve estar funcionando sem erros.
- Todos os campos devem ser validados conforme descrito.
- Nenhum campo pode conter caracteres maliciosos.
- O envio do e-mail deve ser feito através de um repository chamado como bean dentro da rota Camel.
- Respostas de erro e sucesso devem ser claras e informativas.

## 🎯 Extra (opcional)
- Implementar autenticação no endpoint (por exemplo: Basic Auth ou Token JWT).
- Persistir no banco de dados todas as requisições de envio de e-mail que forem realizadas com sucesso.
- Adicionar novos campos opcionais como cc e bcc no e-mail.

| ⚡ **Importante**: Concentre-se principalmente em entender como as rotas e os beans no Apache Camel funcionam!
