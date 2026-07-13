# Cenários de Teste — Restful Booker API

## Cenário 1 — Autenticação

**Objetivo:** Validar a geração e rejeição de tokens de acesso.

| ID | Descrição | Tipo |
|---|---|---|
| CT001 | Gerar token com credenciais válidas | Positivo |
| CT002 | Tentar gerar token com credenciais inválidas | Negativo |

---

## Cenário 2 — CRUD de Reservas

**Objetivo:** Validar o fluxo completo de criação, consulta, atualização e exclusão de reservas.

| ID | Descrição | Tipo |
|---|---|---|
| CT003 | Listar todas as reservas | Positivo |
| CT004 | Criar reserva com dados válidos | Positivo |
| CT005 | Consultar reserva existente pelo ID | Positivo |
| CT006 | Consultar reserva com ID inexistente | Negativo |
| CT007 | Criar reserva com campos obrigatórios ausentes | Negativo |
| CT008 | Criar reserva com formato de data inválido | Negativo |
| CT009 | Atualizar reserva existente com token válido | Positivo |
| CT010 | Tentar atualizar reserva sem token | Negativo |
| CT011 | Tentar atualizar reserva inexistente | Negativo |
| CT012 | Excluir reserva existente com token válido | Positivo |
| CT013 | Tentar excluir reserva sem token | Negativo |
| CT014 | Tentar excluir reserva inexistente | Negativo |

---

## Cenário 3 — Validações Gerais

**Objetivo:** Validar contratos JSON, códigos HTTP e tratamento de erros.

| ID | Descrição | Tipo |
|---|---|---|
| CT015 | Validar contrato JSON da resposta de criação | Positivo |
| CT016 | Validar contrato JSON da resposta de consulta | Positivo |
| CT017 | Validar códigos HTTP e headers | Positivo |
| CT018 | Validar tratamento de JSON malformado | Negativo |

---

## Encadeamento entre Requisições

```
CT001 → salva {{token}}
CT004 → salva {{bookingId}}
CT005 → usa {{bookingId}}
CT009 → usa {{bookingId}} + {{token}}
CT012 → usa {{bookingId}} + {{token}}
```
