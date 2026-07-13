# Casos de Teste — Restful Booker API

---

## CT001 - Gerar Token de Acesso

| Campo | Valor |
|---|---|
| **ID** | CT001 |
| **Título** | Gerar token com credenciais válidas |
| **Método** | POST |
| **Endpoint** | `/auth` |
| **Tipo** | Positivo |
| **Pré-condição** | API disponível, credenciais válidas configuradas no ambiente |

**Body:**
```json
{
  "username": "{{username}}",
  "password": "{{password}}"
}
```

**Resultado Esperado:**
- Status: `200 OK`
- Corpo contém campo `token` do tipo string, não vazio
- Token salvo na variável `{{token}}`

---

## CT002 - Gerar Token com Credenciais Inválidas

| Campo | Valor |
|---|---|
| **ID** | CT002 |
| **Título** | Tentar autenticação com credenciais inválidas |
| **Método** | POST |
| **Endpoint** | `/auth` |
| **Tipo** | Negativo |

**Body:**
```json
{
  "username": "usuario_invalido",
  "password": "senha_invalida"
}
```

**Resultado Esperado:**
- Status: `200`
- Corpo contém `"reason": "Bad credentials"`
- Campo `token` não presente

---

## CT003 - Listar Todas as Reservas

| Campo | Valor |
|---|---|
| **ID** | CT003 |
| **Título** | Listar todas as reservas |
| **Método** | GET |
| **Endpoint** | `/booking` |
| **Tipo** | Positivo |

**Resultado Esperado:**
- Status: `200 OK`
- Corpo é um array
- Array contém ao menos um item com campo `bookingid`

---

## CT004 - Criar Reserva com Dados Válidos

| Campo | Valor |
|---|---|
| **ID** | CT004 |
| **Título** | Criar reserva com dados completos e válidos |
| **Método** | POST |
| **Endpoint** | `/booking` |
| **Tipo** | Positivo |
| **Pós-condição** | `{{bookingId}}` salvo no ambiente |

**Body:**
```json
{
  "firstname": "Daniel",
  "lastname": "Souza",
  "totalprice": 500,
  "depositpaid": true,
  "bookingdates": {
    "checkin": "2025-01-10",
    "checkout": "2025-01-15"
  },
  "additionalneeds": "Café da manhã"
}
```

**Resultado Esperado:**
- Status: `200 OK`
- Corpo contém `bookingid` (number) e `booking` (object)
- Dados retornados correspondem ao enviado

---

## CT005 - Consultar Reserva Existente

| Campo | Valor |
|---|---|
| **ID** | CT005 |
| **Título** | Consultar reserva pelo ID gerado no CT004 |
| **Método** | GET |
| **Endpoint** | `/booking/{{bookingId}}` |
| **Tipo** | Positivo |
| **Pré-condição** | CT004 executado com sucesso |

**Resultado Esperado:**
- Status: `200 OK`
- Corpo contém `firstname: "Daniel"` e `bookingdates`

---

## CT006 - Consultar Reserva Inexistente

| Campo | Valor |
|---|---|
| **ID** | CT006 |
| **Título** | Consultar reserva com ID que não existe |
| **Método** | GET |
| **Endpoint** | `/booking/999999` |
| **Tipo** | Negativo |

**Resultado Esperado:**
- Status: `404 Not Found`
- Corpo indica recurso não encontrado

---

## CT007 - Criar Reserva com Campos Obrigatórios Ausentes

| Campo | Valor |
|---|---|
| **ID** | CT007 |
| **Título** | Criar reserva omitindo campos obrigatórios |
| **Método** | POST |
| **Endpoint** | `/booking` |
| **Tipo** | Negativo |
| **Bug Relacionado** | BUG002 |

**Body:**
```json
{
  "firstname": "Daniel"
}
```

**Resultado Esperado:**
- Status: `400 Bad Request` *(esperado pelo padrão REST)*
- **Comportamento atual:** `500 Internal Server Error` → **BUG002**

---

## CT008 - Criar Reserva com Formato de Data Inválido

| Campo | Valor |
|---|---|
| **ID** | CT008 |
| **Título** | Criar reserva com datas em formato inválido |
| **Método** | POST |
| **Endpoint** | `/booking` |
| **Tipo** | Negativo |
| **Bug Relacionado** | BUG001 |

**Body:**
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

**Resultado Esperado:**
- Status: `400 Bad Request`
- **Comportamento atual:** `200 OK` com dados aceitos → **BUG001**

---

## CT009 - Atualizar Reserva Existente com Token

| Campo | Valor |
|---|---|
| **ID** | CT009 |
| **Título** | Atualizar reserva com token válido |
| **Método** | PUT |
| **Endpoint** | `/booking/{{bookingId}}` |
| **Tipo** | Positivo |
| **Header** | `Cookie: token={{token}}` |

**Resultado Esperado:**
- Status: `200 OK`
- Dados atualizados retornados corretamente

---

## CT010 - Atualizar Reserva Existente sem Token

| Campo | Valor |
|---|---|
| **ID** | CT010 |
| **Título** | Tentar atualizar reserva sem autenticação |
| **Método** | PUT |
| **Endpoint** | `/booking/{{bookingId}}` |
| **Tipo** | Negativo |

**Resultado Esperado:**
- Status: `403 Forbidden`

---

## CT011 - Atualizar Reserva Inexistente

| Campo | Valor |
|---|---|
| **ID** | CT011 |
| **Título** | Tentar atualizar reserva com ID inexistente |
| **Método** | PUT |
| **Endpoint** | `/booking/999999` |
| **Tipo** | Negativo |
| **Header** | `Cookie: token={{token}}` |

**Resultado Esperado:**
- Status: `405 Method Not Allowed`

---

## CT012 - Excluir Reserva Existente com Token

| Campo | Valor |
|---|---|
| **ID** | CT012 |
| **Título** | Excluir reserva com token válido |
| **Método** | DELETE |
| **Endpoint** | `/booking/{{bookingId}}` |
| **Tipo** | Positivo |
| **Header** | `Cookie: token={{token}}` |

**Resultado Esperado:**
- Status: `201 Created`
- Corpo: `Created`

---

## CT013 - Excluir Reserva Existente sem Token

| Campo | Valor |
|---|---|
| **ID** | CT013 |
| **Título** | Tentar excluir reserva sem autenticação |
| **Método** | DELETE |
| **Endpoint** | `/booking/{{bookingId}}` |
| **Tipo** | Negativo |

**Resultado Esperado:**
- Status: `403 Forbidden`

---

## CT014 - Excluir Reserva Inexistente

| Campo | Valor |
|---|---|
| **ID** | CT014 |
| **Título** | Tentar excluir reserva com ID inexistente |
| **Método** | DELETE |
| **Endpoint** | `/booking/999999` |
| **Tipo** | Negativo |
| **Header** | `Cookie: token={{token}}` |

**Resultado Esperado:**
- Status: `405 Method Not Allowed`

---

## CT015 - Validar Contrato JSON da Criação

| Campo | Valor |
|---|---|
| **ID** | CT015 |
| **Título** | Validar contrato JSON da resposta de criação |
| **Método** | POST |
| **Endpoint** | `/booking` |
| **Tipo** | Positivo |

**Resultado Esperado:**
- `bookingid`: number
- `booking.firstname`: string
- `booking.lastname`: string
- `booking.totalprice`: number
- `booking.depositpaid`: boolean
- `booking.bookingdates.checkin`: string
- `booking.bookingdates.checkout`: string

---

## CT016 - Validar Contrato JSON da Consulta

| Campo | Valor |
|---|---|
| **ID** | CT016 |
| **Título** | Validar contrato JSON da resposta de consulta |
| **Método** | GET |
| **Endpoint** | `/booking/{{bookingId}}` |
| **Tipo** | Positivo |

**Resultado Esperado:**
- Todos os campos obrigatórios presentes: `firstname`, `lastname`, `totalprice`, `depositpaid`, `bookingdates`
- Tipos de dados corretos em cada campo

---

## CT017 - Validar Códigos HTTP

| Campo | Valor |
|---|---|
| **ID** | CT017 |
| **Título** | Validar status HTTP e headers do endpoint principal |
| **Método** | GET |
| **Endpoint** | `/booking` |
| **Tipo** | Positivo |

**Resultado Esperado:**
- Status: `200 OK`
- `Content-Type`: `application/json`
- Tempo de resposta abaixo de 5000ms

---

## CT018 - Validar Tratamento de Erros

| Campo | Valor |
|---|---|
| **ID** | CT018 |
| **Título** | Validar tratamento de JSON malformado |
| **Método** | POST |
| **Endpoint** | `/booking` |
| **Tipo** | Negativo |

**Body:** JSON inválido / malformado

**Resultado Esperado:**
- Status: `400`, `415` ou `500`
- Não retorna `200`
