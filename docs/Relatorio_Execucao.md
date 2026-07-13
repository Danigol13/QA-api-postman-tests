# Relatório de Execução — Restful Booker API

| Campo | Valor |
|---|---|
| **Data de Execução** | 2025-07-13 |
| **Executor** | Daniel Bernardo de Souza |
| **Ambiente** | https://restful-booker.herokuapp.com |
| **Ferramenta** | Postman |
| **Collection** | RestfulBooker.postman_collection.json |

---

## Resultado Geral

| Métrica | Resultado |
|---|---|
| Casos Planejados | 18 |
| Casos Executados | 18 |
| Casos Aprovados | 16 |
| Casos Reprovados | 2 |
| Defeitos Registrados | 2 |
| Taxa de Execução | 100% |
| Taxa de Aprovação | 88,9% |

---

## Resultado por Caso de Teste

| ID | Título | Método | Status Esperado | Status Obtido | Resultado |
|---|---|---|---|---|---|
| CT001 | Gerar Token de Acesso | POST | 200 | 200 | ✅ Aprovado |
| CT002 | Gerar Token com Credenciais Inválidas | POST | 200 + reason | 200 + reason | ✅ Aprovado |
| CT003 | Listar Todas as Reservas | GET | 200 | 200 | ✅ Aprovado |
| CT004 | Criar Reserva com Dados Válidos | POST | 200 | 200 | ✅ Aprovado |
| CT005 | Consultar Reserva Existente | GET | 200 | 200 | ✅ Aprovado |
| CT006 | Consultar Reserva Inexistente | GET | 404 | 404 | ✅ Aprovado |
| CT007 | Criar Reserva sem Campos Obrigatórios | POST | 400 | 500 | ❌ Reprovado — BUG002 |
| CT008 | Criar Reserva com Data Inválida | POST | 400 | 200 | ❌ Reprovado — BUG001 |
| CT009 | Atualizar Reserva com Token | PUT | 200 | 200 | ✅ Aprovado |
| CT010 | Atualizar Reserva sem Token | PUT | 403 | 403 | ✅ Aprovado |
| CT011 | Atualizar Reserva Inexistente | PUT | 405 | 405 | ✅ Aprovado |
| CT012 | Excluir Reserva com Token | DELETE | 201 | 201 | ✅ Aprovado |
| CT013 | Excluir Reserva sem Token | DELETE | 403 | 403 | ✅ Aprovado |
| CT014 | Excluir Reserva Inexistente | DELETE | 405 | 405 | ✅ Aprovado |
| CT015 | Validar Contrato JSON da Criação | POST | 200 + contrato | 200 + contrato | ✅ Aprovado |
| CT016 | Validar Contrato JSON da Consulta | GET | 200 + contrato | 200 + contrato | ✅ Aprovado |
| CT017 | Validar Códigos HTTP | GET | 200 | 200 | ✅ Aprovado |
| CT018 | Validar Tratamento de Erros | POST | 4xx/5xx | 500 | ✅ Aprovado |

---

## Defeitos Encontrados

| ID | CT | Descrição | Severidade |
|---|---|---|---|
| BUG001 | CT008 | API aceita data inválida e retorna 200 | Alta |
| BUG002 | CT007 | API retorna 500 para campos obrigatórios ausentes | Alta |

---

## Observações

- O encadeamento de requisições funcionou corretamente: `{{token}}` e `{{bookingId}}` foram propagados entre os CTs.
- Os dois defeitos identificados representam falhas de validação de entrada na API.
- A API pública pode apresentar instabilidade pontual — recomenda-se reexecução em caso de timeout.
