# efeBank

Criar a variavel de ambiente:

DATABASE_URL="mysql://root@localhost:3306/EFEbank"

Rodar o compose:
docker-compose up -d 

link do front:https://cozy-manatee-7df465.netlify.app/


# API Efebank - Transações Bancárias

Esta API permite realizar transações bancárias como crédito, débito, e consultar informações de contas bancárias. Abaixo estão os detalhes de todos os endpoints disponíveis, incluindo exemplos de requisições e respostas.

## Índice

- [Creditar Conta](#post-transactioncredit)
- [Debitar Conta](#post-transactiondebit)

---

## `POST /transaction/credit`

Este endpoint realiza uma transação de **crédito** para a conta bancária especificada.

### Request
Pode utilziar esse json tanto para debito ou credito

```json
{
  "accountNumber": "1234567890",
  "amount": "200.00",
  "counterpartyBankCode": "001",
  "counterpartyBankName": "Banco Exemplo"
}


# API de Conta Bancária

Este documento descreve as rotas disponíveis na API de Conta Bancária.

## Endpoints

### Criar uma Conta Bancária
**POST /bank-account**
- **Body:**
  ```json
  {
  {"branch": "123",
  "type": "CURRENT",
  "holderName": "John Doe",
  "holderEmail": "john.doe@example.com",
  "holderDocument": "12345678901",
  "holderType": "NATURAL",
  "status": "ACTIVE"
}
  }
  ```
- **Response:** Conta criada.

### Listar Todas as Contas
**GET /bank-account/findAll**
- **Response:** Lista de contas cadastradas.

### Buscar Conta por Número
**GET /bank-account/findByNumber/{accountNumber}**
- **Params:** `accountNumber`
- **Response:** Detalhes da conta sem saldo.

### Buscar Contas por Agência
**GET /bank-account/findByBranch/{branch}**
- **Params:** `branch`
- **Response:** Lista de contas da agência.

### Buscar Contas por Titular
**GET /bank-account/findByHolder/{document}**
- **Params:** `document`
- **Response:** Lista de contas do titular.

### Atualizar Email da Conta
**PATCH /bank-account/updateEmail/{accountNumber}**
- **Params:** `accountNumber`
- **Body:**
  ```json
  {
    "email": "string"
  }
  ```
- **Response:** Conta com email atualizado.

### Atualizar Status da Conta
**PATCH /bank-account/{accountNumber}/status**
- **Params:** `accountNumber`
- **Body:**
  ```json
  {
    "status": "ACTIVE" | "INACTIVE"
  }
  ```
- **Response:** Conta com status atualizado.

### Consultar Saldo da Conta
**GET /bank-account/{accountNumber}/balance**
- **Params:** `accountNumber`
- **Response:**
  ```json
  {
    "availableAmount": "number",
    "blockedAmount": "number"
  }
  ```

### Bloquear Valor da Conta
**PATCH /bank-account/{accountNumber}/hold**
- **Params:** `accountNumber`
- **Body:**
  ```json
  {
    "amount": "number"
  }
  ```
- **Response:** Conta com valor bloqueado.

### Liberar Valor da Conta
**PATCH /bank-account/{accountNumber}/release**
- **Params:** `accountNumber`
- **Body:**
  ```json
  {
    "amount": "number"
  }
  ```
- **Response:** Conta com valor liberado.

### Encerrar Conta
**DELETE /bank-account/{accountNumber}**
- **Params:** `accountNumber`
- **Response:** Conta encerrada com sucesso.

