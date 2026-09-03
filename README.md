# iClips

### MCP para iClips, o financeiro e as horas da sua agência em linguagem natural

Converse com o **iClips** da sua agência a partir do Claude, do ChatGPT ou de qualquer cliente MCP. Roda sobre a **API pública oficial do iClips**, com a **chave da sua própria agência**. A cunha aqui é o que costuma virar planilha: o **financeiro completo** (contas bancárias, contas a pagar e a receber com vencimento por parcela, notas fiscais emitidas com os impostos retidos) e a **extração de horas apontadas**, descendo até quem executou cada etapa, quanto tempo levou e de qual departamento é. Também cria e atualiza jobs, peças e tarefas, e marca item de checklist de produção. **Não afiliado ao iClips.**

- 💰 **O financeiro que vira planilha** — contas bancárias, contas a pagar e a receber com o vencimento de cada parcela, notas fiscais emitidas com ISS, PIS, COFINS, INSS, IR e CSLL retidos
- ⏱️ **Horas apontadas por pessoa e por peça** — a hierarquia inteira de projeto, peça, workflow e atividade, com executor, departamento e tempo gasto
- 🗂️ **Jobs e peças, de ida e volta** — cria e atualiza projetos, vincula peças do catálogo, adiciona tarefas e marca item de checklist de produção
- 🎯 **Filtra do jeito que a agência pensa** — por cliente, fornecedor, categoria, indicador de DRE, centro de custo, conta bancária ou job específico
- 🔒 **Financeiro é somente leitura** — o iClips não expõe escrita no financeiro, então dinheiro só se mexe dentro do iClips
- 💬 **Funciona com qualquer cliente MCP**: Claude Desktop, ChatGPT, Cursor, VS Code, Cline, Continue

[English version](README.en.md) · [Documentação completa](docs/) · [Skill pra agentes](skills/)

---

## Instalar em 1 clique

### Claude (Web e Desktop)

A Anthropic unificou a instalação de MCPs em `claude.ai/customize/connectors`. **O mesmo link serve pra Claude Web e Claude Desktop** (basta estar logado):

[➕ Abrir no Claude e conectar](https://claude.ai/new?modal=add-custom-connector#settings/customize-connectors)

**Manual** (se o deeplink não abrir): [claude.ai/customize/connectors](https://claude.ai/customize/connectors?surface=cowork) → **+** → **Adicionar conector personalizado** → cole **Nome** `iClips` e **URL** `https://api.mcp.ai/p_iclips`.

### Cursor

[➕ Instalar iClips no Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=iclips&config=eyJ1cmwiOiJodHRwczovL2FwaS5tY3AuYWkvcF9pY2xpcHMifQ==)

### VS Code (Copilot Chat)

[➕ Instalar iClips no VS Code](vscode:mcp/install?name=iclips&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fapi.mcp.ai%2Fp_iclips%22%7D)

### ChatGPT, Manus, OpenClaw e mais 40+ clientes

Funciona em qualquer cliente MCP que suporte **MCP over HTTP**. A URL do servidor é sempre:

```
https://api.mcp.ai/p_iclips
```

Detalhes por cliente: [INSTALL.md](INSTALL.md).

---

## Exemplos de uso

```
Quanto a agência tem a pagar neste mês, agrupado por fornecedor?
Quantas horas cada pessoa apontou nas peças do cliente X em janeiro?
Liste as notas fiscais emitidas no trimestre com o ISS retido de cada uma
Quais contas a receber vencem nos próximos 15 dias?
Crie um job para o cliente 42 com as tarefas de briefing e aprovação
Quais etapas de workflow tiveram refação no mês passado?
```

---

## 24 ferramentas disponíveis

| Tool | Descrição |
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

Detalhe de cada tool: [docs/ferramentas.md](docs/ferramentas.md)


---

## O que dá para perguntar

| Área | Cobertura | Escrita |
|---|---|---|
| **Financeiro** | Contas bancárias ativas, lançamentos de entrada e saída, contas a pagar e a receber com vencimento por parcela, categorias com indicador de DRE, centros de custo rateados, destinatário e fornecedor | Somente leitura |
| **Notas fiscais** | Notas emitidas com valor bruto e líquido, base de cálculo, alíquota e valor do ISS, retenções de PIS, COFINS, INSS, IR e CSLL, tomador, emitente, RPS e motivo de cancelamento | Somente leitura |
| **Jobs (projetos)** | Criar, atualizar e excluir projetos, com cliente ou grupo de clientes, status, prioridade, verba, responsável e auxiliar | Leitura e escrita |
| **Peças** | Catálogo da agência com busca por nome, categoria e template base, workflow e checklist completos | Leitura e escrita |
| **Peças e tarefas do job** | Vincular peça do catálogo a um projeto, criar e atualizar tarefas, marcar item do checklist de produção | Leitura e escrita |
| **Templates e categorias** | Modelos de workflow configurados na agência e categorias de peça, que alimentam a criação de peças novas | Somente leitura |
| **Extração para BI** | Hierarquia completa de projeto, peça, workflow, atividade e tarefa, com apontamento de horas, executor, departamento e refação | Somente leitura |

### Antes de conectar, três avisos honestos

1. **A chave exige plano PRO e permissão de administrador.** Ela sai em
   Avatar, CHAVE DE API, dentro do iClips. Se a opção não aparece para você, ou
   o seu usuário não é administrador, ou a agência não está no plano PRO. Sem a
   chave não há o que conectar, com nenhuma ferramenta.
2. **O financeiro é somente leitura, e isso é decisão do iClips.** A API pública
   dele não expõe endpoint de escrita no financeiro. Ninguém cria, altera ou
   apaga lançamento por fora do sistema, nem nós.
3. **A extração de horas tem limite de ritmo.** O iClips permite 10 requisições
   por minuto nesse endereço e janelas de até 31 dias por consulta. Relatório de
   ano inteiro sai mês a mês, não num pedido só. O MCP já respeita as duas
   regras e avisa antes de gastar a chamada, em vez de devolver erro do
   servidor.

---

## Preços

Cobrança por conexão ativa. Veja [docs/precos.md](docs/precos.md).

---

## Privacidade & LGPD

- **Sub-processadores**: o LLM host que você escolher (Claude, ChatGPT, Cursor, agente próprio). Lista completa em [docs/privacidade-lgpd.md](docs/privacidade-lgpd.md).
- Os dados retornados pelas tools são enviados ao **LLM host que você escolher**, sub-processador fora do nosso controle. Recomendamos planos com opt-out de treinamento.

---

## Perguntas frequentes

**É o MCP oficial do iClips?**
Não. Este é um MCP **independente**, que fala com a API pública oficial do iClips usando a chave da sua própria agência. **Não é afiliado ao iClips** e não implica parceria. O iClips tem o MCP dele, focado em squads, projetos e peças; este cobre a parte que a API pública expõe e que costuma virar planilha: o módulo financeiro inteiro e a extração de horas apontadas. iClips é marca do seu titular, citada aqui de forma nominativa.

**Que dados vocês acessam?**
Só os que a **chave da sua agência** já alcança. O financeiro é somente leitura por decisão do próprio iClips. Em projetos e peças há escrita, e ela é explícita: criar job, vincular peça, criar tarefa, marcar checklist. Nada acontece sem você pedir.

**Onde fica a minha chave?**
Cifrada, e usada só no cabeçalho de autenticação das chamadas à API pública do iClips. Ela não aparece em resposta de ferramenta nem em log.

**Não acho a opção CHAVE DE API no meu iClips.**
Ela só aparece para usuários com permissão de **administrador**, e a API pública está disponível no **plano PRO**. Se você é administrador e mesmo assim não vê a opção, o caminho é falar com o time do iClips sobre o plano da sua agência.

**Dá para puxar o relatório de horas do ano inteiro de uma vez?**
Não em um pedido só, e o limite é do iClips: a extração aceita janelas de até 31 dias e 10 requisições por minuto por chave. Peça mês a mês. O MCP valida a janela antes de chamar, então você recebe uma orientação clara em vez de um erro do servidor.

**Minha agência tem mais de uma conta no iClips. Funciona?**
Funciona. Conecte uma chave por agência e diga na conversa qual delas você quer. Cada conexão fica separada, e uma chave que expira não derruba as outras.

**Dá para lançar uma conta a pagar pelo chat?**
Não. O iClips não expõe escrita no módulo financeiro na API pública, então esse caminho não existe para nenhuma integração. Consulta, sim; lançamento, dentro do iClips.


---

## Suporte

- 📧 [iclips@mcp.ai](mailto:iclips@mcp.ai)
- 🐛 [GitHub Issues](https://github.com/mcp-dir/iclips-mcp/issues)
- 📄 [docs/](docs/)

---

## Licença

MIT — veja [LICENSE](LICENSE). O servidor MCP em `api.mcp.ai/p_iclips` é proprietário (hosted); este repositório (manifestos, docs, skills) é MIT.
