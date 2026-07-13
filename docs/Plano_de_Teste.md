# Plano de Teste — Restful Booker API

## 1. Identificação

| Campo | Informação |
|---|---|
| Projeto | QA API Tests — Restful Booker |
| Versão | 1.0 |
| Autor | Daniel Bernardo de Souza |
| Data | 2025-07-13 |
| Ferramenta | Postman |

---

## 2. Objetivo

Validar os endpoints REST da API **Restful Booker** (`https://restful-booker.herokuapp.com`), cobrindo operações de autenticação e CRUD de reservas, com foco em:

- Validação funcional dos endpoints
- Testes positivos e negativos
- Validação de contratos JSON
- Validação de códigos de resposta HTTP
- Identificação e documentação de defeitos

---

## 3. Escopo

### 3.1 Em escopo

| Endpoint | Método | Descrição |
|---|---|---|
| `/auth` | POST | Geração de token de acesso |
| `/booking` | GET | Listagem de reservas |
| `/booking` | POST | Criação de reserva |
| `/booking/{id}` | GET | Consulta de reserva por ID |
| `/booking/{id}` | PUT | Atualização de reserva |
| `/booking/{id}` | DELETE | Exclusão de reserva |

### 3.2 Fora do escopo

- Testes de carga e performance
- Testes de segurança (pentest)
- Testes de PATCH (endpoint não documentado)

---

## 4. Critérios de Entrada

- Ambiente da API disponível (`https://restful-booker.herokuapp.com/apidoc`)
- Postman instalado com o ambiente `Ambiente-RestfulBooker` configurado
- Credenciais válidas disponíveis (`admin` / `password123`)

---

## 5. Critérios de Saída

- Todos os 18 casos de teste executados
- Defeitos encontrados documentados em Bug Reports
- Relatório de execução gerado

---

## 6. Estratégia de Teste

### 6.1 Técnicas utilizadas

- **Particionamento de equivalência**: valores válidos e inválidos para cada campo
- **Análise de valor limite**: datas de check-in e check-out
- **Teste de contrato**: validação de tipos e estrutura do JSON de resposta
- **Encadeamento de requisições**: token → bookingId → atualização → exclusão

### 6.2 Tipos de teste

| Tipo | CTs |
|---|---|
| Positivo | CT001, CT003, CT004, CT005, CT009, CT012, CT015, CT016, CT017 |
| Negativo | CT002, CT006, CT007, CT008, CT010, CT011, CT013, CT014, CT018 |

---

## 7. Ambiente

| Item | Valor |
|---|---|
| URL Base | `https://restful-booker.herokuapp.com` |
| Documentação | `https://restful-booker.herokuapp.com/apidoc` |
| Ferramenta | Postman (versão mais recente) |
| Sistema Operacional | Windows 11 |

---

## 8. Riscos e Mitigações

| Risco | Mitigação |
|---|---|
| API pública pode ficar indisponível | Registrar evidências durante a execução |
| Dados criados por outros usuários | Usar bookingId salvo em variável de ambiente |
| Token pode expirar | Executar CT001 sempre antes dos CTs que exigem autenticação |
