# SECOND BRAIN · instruções universais pro agente

> Carregado em TODA conversa. Override de qualquer instrução conflitante.

## O que é

O dono tem um Second Brain em `brain/` (relativo à raiz do projeto · `~/.openclaw/brain/` ou onde foi instalado). Vault de arquivos Markdown que é fonte de verdade pra TUDO permanente: família, negócios, decisões, regras de tom.

**Tu lê e escreve direto via Read e Write tools.**

## Estrutura

```
brain/
├── MAPA.md              ← ÍNDICE COMPLETO · lê primeiro se não souber onde algo está
├── pessoas/             ← perfis (dono.md no mínimo)
├── familia/             ← eventos críticos, rotina sagrada
├── negocios/            ← negócios ativos, decisões operacionais
├── financas/            ← visão geral
├── conteudo/            ← regras de copy/visual se aplicável
├── saude/               ← se aplicável
├── decisoes/            ← decisões grandes com data (YYYY-MM-DD-titulo.md)
├── template/            ← REGRAS UNIVERSAIS (tone, formato-telegram, regras-criticas)
├── daily/               ← log diário opcional (YYYY-MM-DD.md)
└── inbox/               ← coisas não categorizadas · agente raiz varre semanalmente
```

## Regras de USO (HARD)

### 1. LÊ ANTES DE RESPONDER (quando relevante)

Antes de responder pergunta que toque:
- Família · `brain/familia/` + `brain/pessoas/`
- Finanças · `brain/financas/`
- Negócios · `brain/negocios/`
- Decisões grandes · `brain/decisoes/`
- Regra de tom/escopo/formato · `brain/template/`

→ Read direto no arquivo. NÃO chuta. Se não souber qual arquivo, lê `brain/MAPA.md` primeiro.

### 2. ESCREVE QUANDO FATO NOVO PERMANENTE APARECE

Se dono mencionar:
- Decisão grande (mudança de oferta, parar produto, contratar)
- Marco (nascimento, mudança, viagem, evento)
- Fato novo sobre pessoa (papel, contato, mudança)
- Mudança de estado em negócio (pausa, retomada, pivot)
- Mudança de tom/regra/escopo

→ ATUALIZA o arquivo existente OU cria novo em `brain/inbox/<slug>.md` se não tiver pasta clara.

Formato pra `inbox/`:
```
# <título curto>

> origem: <conversa Telegram> · data: YYYY-MM-DD

<conteúdo factual sem inflar>
```

### 3. NÃO DUPLICA

Antes de criar arquivo, Grep no vault pra ver se já existe entry sobre o tema. Se existe, atualiza · não cria novo.

### 4. ATUALIZA `MAPA.md` quando criar arquivo novo

Arquivo órfão (que não tá no MAPA) tende a virar lixo. Toda criação fora de `inbox/` adiciona linha no MAPA.

## Anti-padrões

❌ "Não sei quem é X" → ANTES de dizer isso, Read `brain/pessoas/X.md`. Se não tiver, AÍ pergunta.
❌ Inventar fato sobre dono sem checar vault primeiro
❌ Criar arquivo solto sem adicionar no MAPA
❌ Duplicar entry

## Por que isso existe

Memória fragmentada quebra cross-contexto. Second Brain centraliza tudo num vault único acessível por todos os módulos do agente.
