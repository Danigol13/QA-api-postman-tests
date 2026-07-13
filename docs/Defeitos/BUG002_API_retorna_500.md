# BUG002 — API retorna HTTP 500 para campos obrigatórios ausentes

| Campo | Valor |
|---|---|
| **ID** | BUG002 |
| **Caso de Teste** | CT007 |
| **Data** | 2025-07-13 |
| **Reportado por** | Daniel Bernardo de Souza |
| **Severidade** | Alta |
| **Prioridade** | Alta |
| **Status** | Aberto |
| **Ambiente** | https://restful-booker.herokuapp.com |

---

## Descrição

Ao enviar uma requisição `POST /booking` com apenas o campo `firstname` (omitindo `lastname`, `totalprice`, `depositpaid` e `bookingdates`), a API retorna `500 Internal Server Error`. O comportamento esperado é `400 Bad Request` com uma mensagem indicando os campos obrigatórios ausentes.

---

## Comportamento Esperado

- **Status:** `400 Bad Request`
- **Corpo:** Mensagem de erro listando os campos obrigatórios ausentes (ex: `"lastname is required"`)

---

## Comportamento Atual

- **Status:** `500 Internal Server Error`
- **Corpo:** Resposta genérica de erro interno sem detalhes ao cliente

---

## Passos para Reproduzir

1. Abra o Postman e importe a collection `RestfulBooker.postman_collection.json`
2. Configure o ambiente `Ambiente-RestfulBooker`
3. Execute **CT007 - Criar Reserva com Campos Obrigatórios Ausentes**
4. Observe o status `500 Internal Server Error` na resposta

**Body enviado:**
```json
{
  "firstname": "Daniel"
}
```

---

## Impacto

- Exposição de erro interno do servidor ao cliente (risco de segurança — vazamento de informação)
- Resposta não informativa — o consumidor da API não consegue identificar o que corrigir
- Viola as boas práticas REST (erro 5xx indica problema no servidor, não no cliente)

---

## Evidências

Ver pasta `docs/Defeitos/Evidencias/`

---

## Sugestão de Correção

1. Implementar validação dos campos obrigatórios antes de processar a requisição
2. Retornar `400 Bad Request` com body descritivo listando os campos ausentes
3. Tratar a exceção internamente para não expor stack traces ao cliente
