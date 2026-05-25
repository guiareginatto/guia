# MEMORY — Como o agente grava aprendizados

Memória persistente que sobrevive entre conversas. O agente grava SEM perguntar quando detecta algo importante.

---

## 4 tipos de memória

| Tipo | O que é | Quando grava |
|---|---|---|
| `user_*` | Sobre o dono | Aprende papel, conhecimento, preferência |
| `feedback_*` | Como agir | Dono corrigiu ou validou comportamento |
| `project_*` | Projetos ativos | Aprende sobre lançamento, cliente, oferta vigente |
| `reference_*` | Onde achar info | Links externos, planilhas, painéis |

---

## Estrutura

Cada memória vira um arquivo em `workspace/memory/`. Nome do arquivo segue o padrão `<tipo>_<assunto>.md`.

E tem um índice geral em `workspace/MEMORY.md` (este arquivo serve de exemplo + índice).

---

## Exemplo de `user_*`

Arquivo: `workspace/memory/user_role.md`

```markdown
---
name: Papel do dono
description: Especialista solo em nutrição esportiva, atua há 8 anos, vende mentoria online
type: user
---

Especialista em nutrição esportiva. 8 anos de mercado. Vende mentoria online ticket R$ 4.800 (4 meses, 1 call/semana, grupo WhatsApp). Já tem 200 alunas formadas. Profundo conhecimento técnico, fraco em copy e Z3. Prefere explicação técnica curta a teoria comportamental longa.
```

---

## Exemplo de `feedback_*`

Arquivo: `workspace/memory/feedback_sem_emoji_em_copy.md`

```markdown
---
name: Sem emoji em copy de carrossel
description: Carrossel 3C não leva emoji
type: feedback
---

Em carrossel 3C, não usa emoji em nenhum slide. Reason: dono percebeu que carrossel sem emoji performa 40% melhor no Instagram dela. Validado em 12 testes A/B.

**How to apply**: gerar carrossel para esse dono → zero emoji nos slides. Em legenda do post, OK ter 1.
```

---

## Exemplo de `project_*`

Arquivo: `workspace/memory/project_lancamento_q2_2026.md`

```markdown
---
name: Lançamento Mentoria Performance Q2 2026
description: Lançamento da nova turma (julho 2026), meta 30 vendas
type: project
---

Próximo lançamento: julho 2026. Meta 30 vendas × R$ 4.800 = R$ 144k. Carrinho aberto 7 dias. Pré-venda em 15/jun pra lista interna (300 leads). Stack: Hubla checkout, ActiveCampaign email, Instagram orgânico + 2k ads/dia.

**Why**: precisa fechar mês com 30k+ pra contratar 1ª assistente. Dependência crítica.

**How to apply**: ao sugerir conteúdo até julho, alinhar com tema "performance esportiva". CTA filtrante leva pra Carta. Sem Z2, não tem venda.
```

---

## Exemplo de `reference_*`

Arquivo: `workspace/memory/reference_planilha_clientes.md`

```markdown
---
name: Planilha mestre de clientes
description: Google Sheets com base de leads, status pipeline, histórico
type: reference
---

Google Sheets ID: `1ABC_xyz...`. URL: https://docs.google.com/spreadsheets/d/1ABC_xyz/edit

Aba 1: Leads (nome, telefone, fonte, fase, próximo contato)
Aba 2: Clientes ativos (nome, ticket, mensagem fim)
Aba 3: Histórico de mensagens WhatsApp

**Quando consultar**: dono fala "qual o status da Maria", "quem fechou no mês", "tem lead novo?", "última conversa com X".
```

---

## Quando o agente grava sozinho

Sem perguntar, grava memória se detectar:

1. **Dono corrige comportamento**: "não faz X assim", "para de Y", "não usa Z" → `feedback_*`
2. **Dono valida comportamento não-óbvio**: "isso aí, mantém", "exatamente o que eu queria" → `feedback_*`
3. **Dono explica quem é**: papel, negócio, ticket, avatar → `user_*`
4. **Dono menciona projeto ativo + prazo**: lançamento, oferta vigente, cliente importante → `project_*`
5. **Dono fala onde fica info externa**: "tem isso na planilha X", "vê no Notion Y" → `reference_*`

---

## Quando NÃO grava

- Códigos / paths / convenções deriváveis lendo o repo (use Read)
- Git history, recent changes (use `git log`)
- Solução de bug (commit message + diff já têm)
- Estado temporário (em progresso) — usa Plan/Todos
- Anything em CLAUDE.md

---

## Atualizar memória

Quando uma memória fica errada (dono mudou de ideia, situação evoluiu):

1. Lê a memória existente
2. Edita ou apaga
3. Atualiza este `MEMORY.md` (o índice)

Não acumula memórias contraditórias. Resolve.

---

## Índice de memórias (auto-gerado)

(quando o agente cria/atualiza memória, adiciona linha aqui no formato:)

```
- [Título](memory/arquivo.md) — descrição de 1 linha
```

Exemplo:
```
- [Papel do dono](memory/user_role.md) — Especialista nutrição esportiva, ticket R$ 4.800
- [Sem emoji em carrossel](memory/feedback_sem_emoji.md) — Carrossel 3C zero emoji nos slides
- [Lançamento Q2 2026](memory/project_lancamento_q2_2026.md) — Julho/2026, meta 30 vendas
- [Planilha clientes](memory/reference_planilha_clientes.md) — Sheets 1ABC_xyz com base completa
```

(o índice começa vazio. Conforme o agente aprende, vai crescendo.)
