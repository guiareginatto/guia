# TELEGRAM FORMAT — Regras de output

Aplica a qualquer mensagem que sai pelo Telegram. O bridge sanitiza, mas o agente também evita gerar errado de origem.

## PROIBIDO em mensagens Telegram

- `##` (headers markdown) — Telegram não suporta, vira texto cru
- `**texto**` (negrito duplo) — usa `*texto*` (single asterisk)
- Travessão `—` — denuncia IA e Soft proíbe; usa ponto, vírgula, quebra de linha
- Excesso de emojis (mais de 1 por linha)
- Tabelas com `|` — não fica legível no celular
- Indentação com tabs (usa 2 espaços)
- Walls of text (max 30 linhas; senão split em 2 msg)

## PERMITIDO

- `*texto*` = negrito (use COM MODERAÇÃO)
- `_texto_` = cursiva (datas, contexto)
- `` `código` `` = monospace (SEM ABUSO)
- Emojis: 1 por seção, máximo
- Linha vazia entre blocos
- Separador visual: `━━━━━━━━━━━━━━━━` (16 chars) quando precisar dividir blocos

## Exemplo ❌ ERRADO

```
## Finanças

**PF**
  Saldo: **R$ 185k** 🎯
  Entrada: **R$ 225k** 📈
  Saída: **R$ 85k** 📉

**CNPJ**
  Saldo: **R$ 12k**
```

## Exemplo ✅ CERTO

```
💰 *Finanças 2026-04-29*

💳 *PF*
  Saldo: R$ 185k
  Entrada: R$ 225k
  Saída: R$ 85k

🏢 *CNPJ*
  Saldo: R$ 12k
```

## Enforcement

O bridge sanitiza output (remove `##`, troca `**bold**` por `*bold*`, remove `—`, força max 30 linhas).

Mas o agente também precisa gerar limpo de origem. Bridge é último filtro, não primeiro.

## Áudio

Bot NUNCA responde em áudio. Sempre texto. Detalhe em `TONE.md`.
