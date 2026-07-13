# BUG001 — API aceita criação de reserva com formato de data inválido

| Campo | Valor |
|---|---|
| **ID** | BUG001 |
| **Caso de Teste** | CT008 |
| **Data** | 2025-07-13 |
| **Reportado por** | Daniel Bernardo de Souza |
| **Severidade** | Alta |
| **Prioridade** | Alta |
| **Status** | Aberto |
| **Ambiente** | https://restful-booker.herokuapp.com |

---

## Descrição

A API aceita a criação de reservas contendo datas em formato inválido (ex: `"data-invalida"`) e retorna `200 OK` como se a requisição fosse válida. O comportamento esperado seria rejeitar a requisição com `400 Bad Request` e uma mensagem de erro descritiva.

---

## Comportamento Esperado

- **Status:** `400 Bad Request`
- **Corpo:** Mensagem de erro indicando que o formato de data é inválido (ex: `"checkin must be a valid date in format YYYY-MM-DD"`)

---

## Comportamento Atual

- **Status:** `200 OK`
- **Corpo:** Reserva criada com datas inválidas aceitas

---

## Passos para Reproduzir

1. Abra o Postman e importe a collection `RestfulBooker.postman_collection.json`
2. Configure o ambiente `Ambiente-RestfulBooker`
3. Execute **CT001** para gerar o token
4. Execute **CT008 - Criar Reserva com Formato de Data Inválido**
5. Observe o status `200 OK` na resposta

**Body enviado:**
```json
{
  "firstname": "Daniel",
  "lastname": "Souza",
  "totalprice": 100,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "data-invalida",
    "checkout": "outra-data-invalida"
  }
}
```

---

## Impacto

- Reservas com datas inválidas podem ser persistidas no banco de dados
- Pode causar falhas em processos que dependem de datas válidas (relatórios, notificações, cobranças)
- Compromete a integridade dos dados

---

## Evidências

Ver pasta `docs/Defeitos/Evidencias/`

---

## Sugestão de Correção

Implementar validação de formato de data (`YYYY-MM-DD`) no backend antes de persistir a reserva, retornando `400 Bad Request` com mensagem clara quando o formato for inválido.
