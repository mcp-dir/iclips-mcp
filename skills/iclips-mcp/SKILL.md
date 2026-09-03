---
name: iclips-mcp
description: Consulta e opera o iClips, o ERP e workflow de agências de publicidade e marketing, via MCP. Em leitura: contas bancárias, lançamentos financeiros de entrada e saída, contas a pagar e a receber com vencimento por parcela, notas fiscais emitidas com impostos retidos, catálogo de peças, templates de workflow, categorias, e a hierarquia completa de projetos com apontamento de horas por executor e departamento. Em escrita: criar e atualizar jobs, vincular peças do catálogo a um projeto, criar e atualizar tarefas, e marcar item de checklist de produção. Use quando o usuário perguntar sobre o financeiro da agência, contas a pagar ou a receber, notas fiscais, horas apontadas, produtividade por pessoa, jobs, peças ou workflow no iClips. O módulo financeiro é somente leitura por decisão do provedor. A extração de projetos aceita janelas de até 31 dias e 10 requisições por minuto.
---

# iClips — REST API skill

Você tem acesso à **iClips** REST API na MCP.AI.

> Converse com o **iClips** da sua agência a partir do Claude, do ChatGPT ou de qualquer cliente MCP. Roda sobre a **API pública oficial do iClips**, com a **chave da sua própria agência**. A cunha aqui é o que costuma virar planilha: o **financeiro completo** (contas bancárias, contas a pagar e a receber com vencimento por parcela, notas fiscais emitidas com os impostos retidos) e a **extração de horas apontadas**, descendo até quem executou cada etapa, quanto tempo levou e de qual departamento é. Também cria e atualiza jobs, peças e tarefas, e marca item de checklist de produção. **Não afiliado ao iClips.**

## Base URL

```
https://api.mcp.ai/api/iclips
```

Todo endpoint é um **POST** na Base URL + o path abaixo. Os parâmetros vão no corpo JSON.

## Autenticação

Inclua em toda request:

```
Authorization: Bearer sk_live_...
Content-Type: application/json
```

> Gere sua chave em **https://app.mcp.ai/settings/api-keys** (workspace API key `sk_live_…`, não expira, revogável). Uma única chave serve pra todos os seus MCPs.

## Formato de resposta

```json
{ "ok": true, "tool": "<tool_id>", "result": <payload> }
```

## Exemplo cURL

```bash
curl -X POST https://api.mcp.ai/api/iclips/financial/accounts \
  -H "Authorization: Bearer sk_live_..." \
  -H "Content-Type: application/json" \
  -d '{}'
```

## Reportar problemas

Se um endpoint retornar erro, vazio ou dado inesperado, reporte (não desista calado): **POST /api/iclips/report** com `{ "message": "...", "context"?: "...", "conversation"?: [...] }`. Isso notifica o time da MCP.AI.

## Endpoints (24)

#### `iclips_financial_accounts`

Lista as contas bancárias ativas da agência no iClips (id, nome, isDefault, banco, agência e número da conta). _(POST /api/iclips/financial/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_financial_entries_get`

Lê os lançamentos financeiros do iClips (entradas, saídas e o que está em aberto a pagar e a receber). _(POST /api/iclips/financial/entries/get)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `from` | string | Não | list: início do período em AAAA-MM-DD (obrigatório no list) |
| `to` | string | Não | list: fim do período em AAAA-MM-DD (obrigatório no list, no máximo 366 dias após o from) |
| `date_field` | string | Não | list: qual data o from/to filtra. Padrão entry (entry, payment, competence) |
| `type` | string | Não | list: tipo do lançamento (Entrada, Saída, A Receber, A Pagar) |
| `account_id` | number | Não | list: id da conta bancária (veja iclips_financial_accounts) |
| `category_id` | number | Não | list: id da categoria |
| `dre_indicator` | string | Não | list: indicador de DRE da categoria raiz (DESPESAS OPERACIONAIS, DESPESAS OPERACIONAIS CUSTO VARIÁVEL, DESPESAS OPERACIONAIS CUSTO FIXO, DESPESAS NÃO OPERACIONAIS, IMPOSTOS, PARTICIPAÇÃO NOS LUCROS, RECEITAS OPERACIONAIS, RECEITAS NÃO OPERACIONAIS, RECEITAS TOTAIS, NENHUM, OUTRO) |
| `destination_id` | number | Não | list: id do destinatário (cliente ou fornecedor) |
| `job_id` | number | Não | list: id do job vinculado |
| `limit` | number | Não | list: registros por página, padrão 50, máximo 200 |
| `offset` | number | Não | list: deslocamento da paginação, padrão 0 |
| `entry_ids` | number[] | Não | get: ids dos lançamentos (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_financial_entries_list`

Lê os lançamentos financeiros do iClips (entradas, saídas e o que está em aberto a pagar e a receber). _(POST /api/iclips/financial/entries/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `from` | string | Não | list: início do período em AAAA-MM-DD (obrigatório no list) |
| `to` | string | Não | list: fim do período em AAAA-MM-DD (obrigatório no list, no máximo 366 dias após o from) |
| `date_field` | string | Não | list: qual data o from/to filtra. Padrão entry (entry, payment, competence) |
| `type` | string | Não | list: tipo do lançamento (Entrada, Saída, A Receber, A Pagar) |
| `account_id` | number | Não | list: id da conta bancária (veja iclips_financial_accounts) |
| `category_id` | number | Não | list: id da categoria |
| `dre_indicator` | string | Não | list: indicador de DRE da categoria raiz (DESPESAS OPERACIONAIS, DESPESAS OPERACIONAIS CUSTO VARIÁVEL, DESPESAS OPERACIONAIS CUSTO FIXO, DESPESAS NÃO OPERACIONAIS, IMPOSTOS, PARTICIPAÇÃO NOS LUCROS, RECEITAS OPERACIONAIS, RECEITAS NÃO OPERACIONAIS, RECEITAS TOTAIS, NENHUM, OUTRO) |
| `destination_id` | number | Não | list: id do destinatário (cliente ou fornecedor) |
| `job_id` | number | Não | list: id do job vinculado |
| `limit` | number | Não | list: registros por página, padrão 50, máximo 200 |
| `offset` | number | Não | list: deslocamento da paginação, padrão 0 |
| `entry_ids` | number[] | Não | get: ids dos lançamentos (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_financial_invoices_get`

Lê as notas fiscais de serviço (NFS-e) emitidas pela agência no iClips. _(POST /api/iclips/financial/invoices/get)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `from` | string | Não | list: início do período de emissão em AAAA-MM-DD (obrigatório no list) |
| `to` | string | Não | list: fim do período de emissão em AAAA-MM-DD (obrigatório no list, no máximo 366 dias) |
| `status` | string | Não | list: status da nota fiscal (pending, issued, cancelled, error) |
| `limit` | number | Não | list: registros por página, padrão 50, máximo 200 |
| `offset` | number | Não | list: deslocamento da paginação, padrão 0 |
| `invoice_ids` | number[] | Não | get: ids das notas fiscais (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_financial_invoices_list`

Lê as notas fiscais de serviço (NFS-e) emitidas pela agência no iClips. _(POST /api/iclips/financial/invoices/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `from` | string | Não | list: início do período de emissão em AAAA-MM-DD (obrigatório no list) |
| `to` | string | Não | list: fim do período de emissão em AAAA-MM-DD (obrigatório no list, no máximo 366 dias) |
| `status` | string | Não | list: status da nota fiscal (pending, issued, cancelled, error) |
| `limit` | number | Não | list: registros por página, padrão 50, máximo 200 |
| `offset` | number | Não | list: deslocamento da paginação, padrão 0 |
| `invoice_ids` | number[] | Não | get: ids das notas fiscais (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_job_pieces_write_add`

Vincula uma peça do catálogo a um job existente, ou atualiza uma peça já vinculada a ele. _(POST /api/iclips/job/pieces/write/add)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `job_id` | number | Sim | Id do job |
| `job_piece_id` | number | Não | update: id da peça dentro do job (jobPecaId) |
| `data` | string | Sim | Campos da peça como string JSON |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |
| `job_ids` | number[] | Não | Bulk mode: multiple values for job_id |
| `job_piece_ids` | number[] | Não | Bulk mode: multiple values for job_piece_id |

#### `iclips_job_pieces_write_update`

Vincula uma peça do catálogo a um job existente, ou atualiza uma peça já vinculada a ele. _(POST /api/iclips/job/pieces/write/update)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `job_id` | number | Sim | Id do job |
| `job_piece_id` | number | Não | update: id da peça dentro do job (jobPecaId) |
| `data` | string | Sim | Campos da peça como string JSON |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |
| `job_ids` | number[] | Não | Bulk mode: multiple values for job_id |
| `job_piece_ids` | number[] | Não | Bulk mode: multiple values for job_piece_id |

#### `iclips_job_tasks_write_create`

Cria ou atualiza uma tarefa manual dentro de um job existente no iClips. _(POST /api/iclips/job/tasks/write/create)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `job_id` | number | Sim | Id do job |
| `task_id` | number | Não | update: id da tarefa dentro do job (idTarefaJob) |
| `data` | string | Sim | Campos da tarefa como string JSON |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |
| `job_ids` | number[] | Não | Bulk mode: multiple values for job_id |
| `task_ids` | number[] | Não | Bulk mode: multiple values for task_id |

#### `iclips_job_tasks_write_update`

Cria ou atualiza uma tarefa manual dentro de um job existente no iClips. _(POST /api/iclips/job/tasks/write/update)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `job_id` | number | Sim | Id do job |
| `task_id` | number | Não | update: id da tarefa dentro do job (idTarefaJob) |
| `data` | string | Sim | Campos da tarefa como string JSON |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |
| `job_ids` | number[] | Não | Bulk mode: multiple values for job_id |
| `task_ids` | number[] | Não | Bulk mode: multiple values for task_id |

#### `iclips_jobs_delete`

Exclui jobs (projetos) do iClips. _(POST /api/iclips/jobs/delete)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `job_ids` | number[] | Sim | ids dos jobs a excluir (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_jobs_write_create`

Cria ou atualiza um job (projeto) no iClips. _(POST /api/iclips/jobs/write/create)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `job_id` | number | Não | update: id do job |
| `data` | string | Sim | Campos do job como string JSON |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |
| `job_ids` | number[] | Não | Bulk mode: multiple values for job_id |

#### `iclips_jobs_write_update`

Cria ou atualiza um job (projeto) no iClips. _(POST /api/iclips/jobs/write/update)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `job_id` | number | Não | update: id do job |
| `data` | string | Sim | Campos do job como string JSON |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |
| `job_ids` | number[] | Não | Bulk mode: multiple values for job_id |

#### `iclips_list_accounts`

Lista as agências iClips (chaves de API) ligadas a este install, com id, apelido e nome. _(POST /api/iclips/list/accounts)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_piece_categories_dropdown`

Lista as categorias de peça disponíveis na agência (id e nome). _(POST /api/iclips/piece/categories/dropdown)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_piece_categories_list`

Lista as categorias de peça disponíveis na agência (id e nome). _(POST /api/iclips/piece/categories/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_pieces_delete`

Exclui peças do catálogo do iClips (o provider faz exclusão lógica). _(POST /api/iclips/pieces/delete)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `piece_ids` | number[] | Sim | ids das peças a excluir (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_pieces_get`

Lê o catálogo de peças da agência no iClips. _(POST /api/iclips/pieces/get)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `q` | string | Não | list: busca textual pelo nome da peça |
| `categoria` | string | Não | list: filtro por id de categoria |
| `status` | string | Não | list: filtro por status da peça |
| `basedOnTemplateId` | string | Não | list: filtro por id do template de workflow base |
| `page` | number | Não | list: número da página, padrão 1 |
| `pageSize` | number | Não | list: itens por página, padrão 20 |
| `piece_ids` | number[] | Não | get: ids das peças (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_pieces_list`

Lê o catálogo de peças da agência no iClips. _(POST /api/iclips/pieces/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `q` | string | Não | list: busca textual pelo nome da peça |
| `categoria` | string | Não | list: filtro por id de categoria |
| `status` | string | Não | list: filtro por status da peça |
| `basedOnTemplateId` | string | Não | list: filtro por id do template de workflow base |
| `page` | number | Não | list: número da página, padrão 1 |
| `pageSize` | number | Não | list: itens por página, padrão 20 |
| `piece_ids` | number[] | Não | get: ids das peças (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_pieces_write_checklist`

Cria ou atualiza uma peça no catálogo do iClips, ou marca um item do checklist. _(POST /api/iclips/pieces/write/checklist)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `piece_id` | number | Não | update e checklist: id da peça |
| `data` | string | Sim | Campos da peça como string JSON |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |
| `piece_ids` | number[] | Não | Bulk mode: multiple values for piece_id |

#### `iclips_pieces_write_create`

Cria ou atualiza uma peça no catálogo do iClips, ou marca um item do checklist. _(POST /api/iclips/pieces/write/create)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `piece_id` | number | Não | update e checklist: id da peça |
| `data` | string | Sim | Campos da peça como string JSON |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |
| `piece_ids` | number[] | Não | Bulk mode: multiple values for piece_id |

#### `iclips_pieces_write_update`

Cria ou atualiza uma peça no catálogo do iClips, ou marca um item do checklist. _(POST /api/iclips/pieces/write/update)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `piece_id` | number | Não | update e checklist: id da peça |
| `data` | string | Sim | Campos da peça como string JSON |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |
| `piece_ids` | number[] | Não | Bulk mode: multiple values for piece_id |

#### `iclips_projects_extract`

Extrai do iClips a hierarquia completa de projetos de um período: Jobs, Peças, Workflows, Atividades e Tarefas, até os apontamentos de hora. _(POST /api/iclips/projects/extract)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `dataInicio` | string | Sim | Início do período, AAAA-MM-DDTHH:mm:ss (ou AAAA-MM-DD) |
| `dataFim` | string | Sim | Fim do período, no máximo 31 dias após o dataInicio |
| `idCliente` | number | Não | Filtra pelo id do cliente |
| `idGrupoCliente` | number | Não | Filtra pelo id do grupo de clientes |
| `page` | number | Não | Número da página, padrão 1 |
| `pageSize` | number | Não | Itens por página, padrão 20, máximo 50 |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_workflow_templates_get`

Lê os modelos de workflow configurados na agência no iClips. _(POST /api/iclips/workflow/templates/get)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `template_ids` | number[] | Não | get: ids dos templates de workflow (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

#### `iclips_workflow_templates_list`

Lê os modelos de workflow configurados na agência no iClips. _(POST /api/iclips/workflow/templates/list)_

| Parâmetro | Tipo | Obrigatório | Descrição |
|---|---|---|---|
| `template_ids` | number[] | Não | get: ids dos templates de workflow (até 50 por chamada) |
| `account` | string | Não | Quando há mais de uma agência iClips conectada: o id, o apelido ou o nome da conexão. Omita para usar a agência padrão do workspace. Veja iclips_list_accounts. |

---

Este MCP também funciona via **conexão MCP** (Claude / Cursor) em `https://api.mcp.ai/p_iclips` — veja o [README](../../README.md). A skill acima é pra consumir a **REST API** direto (agente próprio / código).
