# Ferramentas

iClips expõe 24 ferramentas.

### 1. `iclips_list_accounts`
**Input**: `account` (opcional)

Lista as agências iClips (chaves de API) ligadas a este install, com id, apelido e nome.

### 2. `iclips_financial_accounts`
**Input**: `account` (opcional)

Lista as contas bancárias ativas da agência no iClips (id, nome, isDefault, banco, agência e número da conta).

### 3. `iclips_financial_entries_list`
**Input**: `from` (opcional), `to` (opcional), `date_field` (opcional), `type` (opcional), `account_id` (opcional), `category_id` (opcional), `dre_indicator` (opcional), `destination_id` (opcional), `job_id` (opcional), `limit` (opcional), `offset` (opcional), `entry_ids` (opcional), `account` (opcional)

Lê os lançamentos financeiros do iClips (entradas, saídas e o que está em aberto a pagar e a receber).

### 4. `iclips_financial_entries_get`
**Input**: `from` (opcional), `to` (opcional), `date_field` (opcional), `type` (opcional), `account_id` (opcional), `category_id` (opcional), `dre_indicator` (opcional), `destination_id` (opcional), `job_id` (opcional), `limit` (opcional), `offset` (opcional), `entry_ids` (opcional), `account` (opcional)

Lê os lançamentos financeiros do iClips (entradas, saídas e o que está em aberto a pagar e a receber).

### 5. `iclips_financial_invoices_list`
**Input**: `from` (opcional), `to` (opcional), `status` (opcional), `limit` (opcional), `offset` (opcional), `invoice_ids` (opcional), `account` (opcional)

Lê as notas fiscais de serviço (NFS-e) emitidas pela agência no iClips.

### 6. `iclips_financial_invoices_get`
**Input**: `from` (opcional), `to` (opcional), `status` (opcional), `limit` (opcional), `offset` (opcional), `invoice_ids` (opcional), `account` (opcional)

Lê as notas fiscais de serviço (NFS-e) emitidas pela agência no iClips.

### 7. `iclips_jobs_write_create`
**Input**: `job_id` (opcional), `data`, `account` (opcional), `job_ids` (opcional)

Cria ou atualiza um job (projeto) no iClips.

### 8. `iclips_jobs_write_update`
**Input**: `job_id` (opcional), `data`, `account` (opcional), `job_ids` (opcional)

Cria ou atualiza um job (projeto) no iClips.

### 9. `iclips_jobs_delete`
**Input**: `job_ids`, `account` (opcional)

Exclui jobs (projetos) do iClips.

### 10. `iclips_job_pieces_write_add`
**Input**: `job_id`, `job_piece_id` (opcional), `data`, `account` (opcional), `job_ids` (opcional), `job_piece_ids` (opcional)

Vincula uma peça do catálogo a um job existente, ou atualiza uma peça já vinculada a ele.

### 11. `iclips_job_pieces_write_update`
**Input**: `job_id`, `job_piece_id` (opcional), `data`, `account` (opcional), `job_ids` (opcional), `job_piece_ids` (opcional)

Vincula uma peça do catálogo a um job existente, ou atualiza uma peça já vinculada a ele.

### 12. `iclips_job_tasks_write_create`
**Input**: `job_id`, `task_id` (opcional), `data`, `account` (opcional), `job_ids` (opcional), `task_ids` (opcional)

Cria ou atualiza uma tarefa manual dentro de um job existente no iClips.

### 13. `iclips_job_tasks_write_update`
**Input**: `job_id`, `task_id` (opcional), `data`, `account` (opcional), `job_ids` (opcional), `task_ids` (opcional)

Cria ou atualiza uma tarefa manual dentro de um job existente no iClips.

### 14. `iclips_pieces_list`
**Input**: `q` (opcional), `categoria` (opcional), `status` (opcional), `basedOnTemplateId` (opcional), `page` (opcional), `pageSize` (opcional), `piece_ids` (opcional), `account` (opcional)

Lê o catálogo de peças da agência no iClips.

### 15. `iclips_pieces_get`
**Input**: `q` (opcional), `categoria` (opcional), `status` (opcional), `basedOnTemplateId` (opcional), `page` (opcional), `pageSize` (opcional), `piece_ids` (opcional), `account` (opcional)

Lê o catálogo de peças da agência no iClips.

### 16. `iclips_pieces_write_create`
**Input**: `piece_id` (opcional), `data`, `account` (opcional), `piece_ids` (opcional)

Cria ou atualiza uma peça no catálogo do iClips, ou marca um item do checklist.

### 17. `iclips_pieces_write_update`
**Input**: `piece_id` (opcional), `data`, `account` (opcional), `piece_ids` (opcional)

Cria ou atualiza uma peça no catálogo do iClips, ou marca um item do checklist.

### 18. `iclips_pieces_write_checklist`
**Input**: `piece_id` (opcional), `data`, `account` (opcional), `piece_ids` (opcional)

Cria ou atualiza uma peça no catálogo do iClips, ou marca um item do checklist.

### 19. `iclips_pieces_delete`
**Input**: `piece_ids`, `account` (opcional)

Exclui peças do catálogo do iClips (o provider faz exclusão lógica).

### 20. `iclips_workflow_templates_list`
**Input**: `template_ids` (opcional), `account` (opcional)

Lê os modelos de workflow configurados na agência no iClips.

### 21. `iclips_workflow_templates_get`
**Input**: `template_ids` (opcional), `account` (opcional)

Lê os modelos de workflow configurados na agência no iClips.

### 22. `iclips_piece_categories_list`
**Input**: `account` (opcional)

Lista as categorias de peça disponíveis na agência (id e nome).

### 23. `iclips_piece_categories_dropdown`
**Input**: `account` (opcional)

Lista as categorias de peça disponíveis na agência (id e nome).

### 24. `iclips_projects_extract`
**Input**: `dataInicio`, `dataFim`, `idCliente` (opcional), `idGrupoCliente` (opcional), `page` (opcional), `pageSize` (opcional), `account` (opcional)

Extrai do iClips a hierarquia completa de projetos de um período: Jobs, Peças, Workflows, Atividades e Tarefas, até os apontamentos de hora.

## Prompts de exemplo

```
Quanto a agência tem a pagar neste mês, agrupado por fornecedor?
Quantas horas cada pessoa apontou nas peças do cliente X em janeiro?
Liste as notas fiscais emitidas no trimestre com o ISS retido de cada uma
Quais contas a receber vencem nos próximos 15 dias?
Crie um job para o cliente 42 com as tarefas de briefing e aprovação
Quais etapas de workflow tiveram refação no mês passado?
```
