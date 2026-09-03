# iClips

### iClips MCP, your agency's finance and logged hours in plain language

Talk to your agency's **iClips** from Claude, ChatGPT or any MCP client. It runs on the **official iClips public API**, with **your own agency's key**. The wedge is the part that usually becomes a spreadsheet: the **full finance module** (bank accounts, payables and receivables with per installment due dates, issued service invoices with the taxes withheld) and the **extraction of logged hours**, down to who executed each step, how long it took and which department they belong to. It also creates and updates jobs, pieces and tasks, and ticks production checklist items. **Not affiliated with iClips.**

- 💰 **The finance that becomes a spreadsheet** — bank accounts, payables and receivables with each installment's due date, issued invoices with ISS, PIS, COFINS, INSS, IR and CSLL withheld
- ⏱️ **Hours logged per person and per piece** — the whole project, piece, workflow and activity hierarchy, with executor, department and time spent
- 🗂️ **Jobs and pieces, both ways** — create and update projects, attach catalog pieces, add tasks and tick production checklist items
- 🎯 **Filters the way an agency thinks** — by client, supplier, category, DRE indicator, cost center, bank account or a specific job
- 🔒 **Finance is read-only** — iClips exposes no write endpoints for finance, so money only moves inside iClips
- 💬 **Works with any MCP client**: Claude Desktop, ChatGPT, Cursor, VS Code, Cline, Continue

[Versão em português](README.md) · [Full docs (PT-BR)](docs/) · [Agent skill](skills/)

---

## One-click install

### Claude (Web and Desktop)

Anthropic unified MCP installation at `claude.ai/customize/connectors`. **The same link works for Claude Web and Claude Desktop** (just be logged in):

[➕ Open in Claude and connect](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (if the deeplink does not open): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Add custom connector** → paste **Name** `iClips` and **URL** `https://api.mcp.ai/p_iclips`.

### Cursor

[➕ Install iClips in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=iclips&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9pY2xpcHMifQ==)

### VS Code (Copilot Chat)

[➕ Install iClips in VS Code](vscode:mcp/install?name=iclips&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_iclips%22%7D)

### ChatGPT, Manus, OpenClaw and 40+ other clients

Works with any MCP client that speaks **MCP over HTTP**. The server URL is always:

```
https://api.mcp.ai/p_iclips
```

Per-client details: [INSTALL.md](INSTALL.md).

---

## Example prompts

```
How much does the agency have payable this month, grouped by supplier?
How many hours did each person log on client X's pieces in January?
List the invoices issued this quarter with the ISS withheld on each
Which receivables fall due in the next 15 days?
Create a job for client 42 with the briefing and approval tasks
Which workflow steps had rework last month?
```

---

## 24 tools available

| Tool | Description |
|---|---|
| `iclips_list_accounts` | Lista as agências iClips (chaves de API) ligadas a este install, com id, apelido e nome. |
| `iclips_financial_accounts` | Lista as contas bancárias ativas da agência no iClips (id, nome, isDefault, banco, agência e número da conta). |
| `iclips_financial_entries_list` | Lê os lançamentos financeiros do iClips (entradas, saídas e o que está em aberto a pagar e a receber). |
| `iclips_financial_entries_get` | Lê os lançamentos financeiros do iClips (entradas, saídas e o que está em aberto a pagar e a receber). |
| `iclips_financial_invoices_list` | Lê as notas fiscais de serviço (NFS-e) emitidas pela agência no iClips. |
| `iclips_financial_invoices_get` | Lê as notas fiscais de serviço (NFS-e) emitidas pela agência no iClips. |
| `iclips_jobs_write_create` | Cria ou atualiza um job (projeto) no iClips. |
| `iclips_jobs_write_update` | Cria ou atualiza um job (projeto) no iClips. |
| `iclips_jobs_delete` | Exclui jobs (projetos) do iClips. |
| `iclips_job_pieces_write_add` | Vincula uma peça do catálogo a um job existente, ou atualiza uma peça já vinculada a ele. |
| `iclips_job_pieces_write_update` | Vincula uma peça do catálogo a um job existente, ou atualiza uma peça já vinculada a ele. |
| `iclips_job_tasks_write_create` | Cria ou atualiza uma tarefa manual dentro de um job existente no iClips. |
| `iclips_job_tasks_write_update` | Cria ou atualiza uma tarefa manual dentro de um job existente no iClips. |
| `iclips_pieces_list` | Lê o catálogo de peças da agência no iClips. |
| `iclips_pieces_get` | Lê o catálogo de peças da agência no iClips. |
| `iclips_pieces_write_create` | Cria ou atualiza uma peça no catálogo do iClips, ou marca um item do checklist. |
| `iclips_pieces_write_update` | Cria ou atualiza uma peça no catálogo do iClips, ou marca um item do checklist. |
| `iclips_pieces_write_checklist` | Cria ou atualiza uma peça no catálogo do iClips, ou marca um item do checklist. |
| `iclips_pieces_delete` | Exclui peças do catálogo do iClips (o provider faz exclusão lógica). |
| `iclips_workflow_templates_list` | Lê os modelos de workflow configurados na agência no iClips. |
| `iclips_workflow_templates_get` | Lê os modelos de workflow configurados na agência no iClips. |
| `iclips_piece_categories_list` | Lista as categorias de peça disponíveis na agência (id e nome). |
| `iclips_piece_categories_dropdown` | Lista as categorias de peça disponíveis na agência (id e nome). |
| `iclips_projects_extract` | Extrai do iClips a hierarquia completa de projetos de um período: Jobs, Peças, Workflows, Atividades e Tarefas, até os apontamentos de hora. |

Details for each tool: [docs/ferramentas.md](docs/ferramentas.md) (PT-BR)


---

## What you can ask

| Area | Coverage | Writes |
|---|---|---|
| **Finance** | Active bank accounts, cash in and out entries, payables and receivables with per installment due dates, categories with DRE indicator, cost center splits, destination and supplier | Read-only |
| **Invoices** | Issued invoices with gross and net amounts, tax base, ISS rate and amount, PIS, COFINS, INSS, IR and CSLL withheld, client, issuer, RPS and cancellation reason | Read-only |
| **Jobs (projects)** | Create, update and delete projects, with client or client group, status, priority, budget, owner and assistant | Read and write |
| **Pieces** | The agency catalog with search by name, category and base template, full workflow and checklist | Read and write |
| **Job pieces and tasks** | Attach a catalog piece to a project, create and update tasks, tick production checklist items | Read and write |
| **Templates and categories** | Workflow templates configured in the agency and piece categories, which feed the creation of new pieces | Read-only |
| **BI extraction** | The full project, piece, workflow, activity and task hierarchy, with logged hours, executor, department and rework | Read-only |

### Three honest notes before you connect

1. **The key requires the PRO plan and admin permission.** You generate it under
   Avatar, CHAVE DE API, inside iClips. If the option is not there, either your
   user is not an administrator or the agency is not on the PRO plan. Without the
   key there is nothing to connect to, with any tool.
2. **Finance is read-only, and that is iClips' decision.** Their public API
   exposes no write endpoints for finance. Nobody creates, changes or deletes an
   entry from outside the system, us included.
3. **The hours extraction is rate limited.** iClips allows 10 requests per minute
   on that endpoint and windows of up to 31 days per query. A full year report
   comes month by month, not in a single request. This MCP already honors both
   rules and says so before spending the call, instead of handing you a server
   error.

---

## Pricing

Billed per connected account. See [docs/precos.md](docs/precos.md) (PT-BR).

---

## Privacy & data protection

- **Sub-processors**: the LLM host you choose (Claude, ChatGPT, Cursor, your own agent). Full list in [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Data returned by the tools is sent to **the LLM host you choose**, a sub-processor outside our control. We recommend plans with training opt-out.

---

## FAQ

**Is this the official iClips MCP?**
No. This is an **independent** MCP that talks to the official iClips public API using your own agency's key. It is **not affiliated with iClips** and implies no partnership. iClips ships its own MCP focused on squads, projects and pieces; this one covers what the public API exposes and what usually ends up in a spreadsheet: the full finance module and the extraction of logged hours. iClips is a trademark of its owner, referenced here nominatively.

**What data do you access?**
Only what **your agency's key** already reaches. Finance is read-only by iClips' own decision. Projects and pieces do allow writes, and they are explicit: create a job, attach a piece, create a task, tick a checklist item. Nothing happens unless you ask.

**Where does my key live?**
Encrypted, and used only in the authentication header of calls to the iClips public API. It never shows up in a tool response or in logs.

**I cannot find the CHAVE DE API option in my iClips.**
It only appears for users with **administrator** permission, and the public API is available on the **PRO plan**. If you are an administrator and still do not see it, the next step is asking the iClips team about your agency's plan.

**Can I pull a full year of logged hours in one go?**
Not in a single request, and the limit is iClips': the extraction accepts windows of up to 31 days and 10 requests per minute per key. Ask month by month. This MCP validates the window before calling, so you get clear guidance instead of a server error.

**My group has more than one iClips account. Does it work?**
Yes. Connect one key per agency and say which one you mean in the conversation. Each connection stays separate, and one expired key does not take the others down.

**Can I create a payable from the chat?**
No. iClips exposes no write endpoints for the finance module in its public API, so that path does not exist for any integration. Querying, yes; posting entries, inside iClips.


---

## Support

- 📧 [iclips@mcp.ai](mailto:iclips@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/iclips-mcp/issues)
- 📄 [docs/](docs/)

---

## License

MIT — see [LICENSE](LICENSE). The MCP server at `api.mcp.ai/p_iclips` is proprietary (hosted); this repo (manifests, docs, skills) is MIT.
