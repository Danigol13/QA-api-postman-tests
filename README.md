# Testes de API REST com Postman — Restful Booker

Projeto desenvolvido com foco em Qualidade de Software (QA), contemplando planejamento, execução e documentação de testes em APIs REST utilizando Postman.

O objetivo é demonstrar um fluxo completo de testes, incluindo validações funcionais, testes negativos, validação de contratos JSON, registro de evidências e documentação de defeitos encontrados durante a execução.

---

## Objetivos

- Validar endpoints REST utilizando Postman
- Executar testes positivos e negativos
- Validar códigos de resposta HTTP
- Validar contratos JSON
- Registrar evidências dos testes executados
- Documentar defeitos encontrados
- Demonstrar boas práticas de QA em APIs

---

## Tecnologias Utilizadas

| Tecnologia | Função |
|---|---|
| Postman | Ferramenta principal de testes |
| REST API | Protocolo de comunicação testado |
| JavaScript | Scripts de validação nos testes |
| JSON | Formato de dados da API |
| Swagger/OpenAPI | Documentação da API |
| Git | Controle de versão |
| GitHub | Hospedagem do repositório |
| Markdown | Documentação do projeto |

---

## API Utilizada

**Restful Booker**
`https://restful-booker.herokuapp.com`

API pública utilizada para estudos e práticas de testes de software.
Documentação: `https://restful-booker.herokuapp.com/apidoc`

---

## Estrutura do Projeto

```
QA-api-tests-postman/
│
├── collections/
│   └── RestfulBooker.postman_collection.json
│
├── environments/
│   └── Ambiente-RestfulBooker.postman_environment.json
│
├── docs/
│   ├── Cenario_de_Teste.md
│   ├── Plano_de_Teste.md
│   ├── Casos_de_Teste.md
│   ├── Relatorio_Execucao.md
│   ├── Registro_de_Defeitos.md
│   │
│   ├── Evidencias/
│   │
│   └── Defeitos/
│       ├── BUG001_API_aceita_data_invalida.md
│       ├── BUG002_API_retorna_500.md
│       └── Evidencias/
│
└── README.md
```

---

## Como Executar

### 1. Importar a Collection

1. Abra o Postman
2. Clique em **Import**
3. Selecione o arquivo `collections/RestfulBooker.postman_collection.json`

### 2. Importar o Ambiente

1. Clique em **Import**
2. Selecione `environments/Ambiente-RestfulBooker.postman_environment.json`
3. Ative o ambiente `Ambiente-RestfulBooker` no canto superior direito

### 3. Executar os Testes

**Ordem recomendada (encadeamento):**

```
CT001 → CT003 → CT004 → CT005 → CT009 → CT012
```

> CT001 gera o `{{token}}` e CT004 gera o `{{bookingId}}`, ambos necessários para os CTs seguintes.

**Executar toda a collection:**
1. Clique nos três pontos da collection
2. Selecione **Run collection**
3. Clique em **Run RestfulBooker**

---

## Casos de Teste

### Autenticação

| ID | Descrição | Tipo |
|---|---|---|
| CT001 | Gerar Token de Acesso | Positivo |
| CT002 | Gerar Token com Credenciais Inválidas | Negativo |

### Reservas

| ID | Descrição | Tipo |
|---|---|---|
| CT003 | Listar Todas as Reservas | Positivo |
| CT004 | Criar Reserva com Dados Válidos | Positivo |
| CT005 | Consultar Reserva Existente | Positivo |
| CT006 | Consultar Reserva Inexistente | Negativo |
| CT007 | Criar Reserva com Campos Obrigatórios Ausentes | Negativo |
| CT008 | Criar Reserva com Formato de Data Inválido | Negativo |
| CT009 | Atualizar Reserva Existente com Token | Positivo |
| CT010 | Atualizar Reserva Existente sem Token | Negativo |
| CT011 | Atualizar Reserva Inexistente | Negativo |
| CT012 | Excluir Reserva Existente com Token | Positivo |
| CT013 | Excluir Reserva Existente sem Token | Negativo |
| CT014 | Excluir Reserva Inexistente | Negativo |

### Validações Gerais

| ID | Descrição | Tipo |
|---|---|---|
| CT015 | Validar Contrato JSON da Criação | Positivo |
| CT016 | Validar Contrato JSON da Consulta | Positivo |
| CT017 | Validar Códigos HTTP | Positivo |
| CT018 | Validar Tratamento de Erros | Negativo |

---

## Resultado da Execução

| Métrica | Resultado |
|---|---|
| Casos Planejados | 18 |
| Casos Executados | 18 |
| Casos Aprovados | 16 |
| Defeitos Registrados | 2 |
| Taxa de Execução | 100% |
| Taxa de Aprovação | 88,9% |

---

## Defeitos Identificados

| ID | Caso de Teste | Descrição | Severidade |
|---|---|---|---|
| BUG001 | CT008 | API aceita criação de reserva com formato de data inválido | Alta |
| BUG002 | CT007 | API retorna HTTP 500 para campos obrigatórios ausentes | Alta |

---

## Postman Flows

### Flow 01 - CRUD Positivo
`Autenticação → Listagem → Criação → Consulta por ID → Atualização → Exclusão`

### Flow 02 - Validação de Entrada
`Credenciais Inválidas → Reserva Inexistente → Campos Ausentes → Data Inválida`

### Flow 03 - Autorização e Recursos
`Atualização sem Token → Exclusão sem Token → Atualização Inexistente → Exclusão Inexistente`

### Flow 04 - Validações Gerais
`Contratos JSON → Códigos HTTP → Tratamento de Erros`

---

## Competências Demonstradas

- Plano de Testes
- Cenários de Teste
- Casos de Teste
- Testes Funcionais
- Testes de API REST
- Testes Positivos e Negativos
- Validação de Contratos JSON
- Validação de Códigos HTTP
- Encadeamento de Requisições
- Scripts de Validação em JavaScript
- Variáveis de Ambiente
- Registro de Evidências
- Gestão de Defeitos
- Documentação Técnica
- Postman Flows
- Git e GitHub

---

## Próximas Evoluções

- [ ] Execução automatizada com Newman
- [ ] Relatórios HTML via Newman
- [ ] Integração com GitHub Actions
- [ ] Pipeline CI/CD para execução automática dos testes

---

## Autor

**Daniel Bernardo de Souza**
QA Engineer
