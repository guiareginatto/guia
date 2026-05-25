# MEMORY — Índice de memórias

Lista do que o agente já aprendeu. Cada item aponta pra um arquivo em `memory/`.

Formato: `- [Título](memory/arquivo.md) — descrição de 1 linha`

Detalhe sobre tipos e quando gravar em `MEMORY_TEMPLATE.md`.

---

## Memórias gravadas

(começa vazio. Conforme o agente conversa, ele adiciona aqui.)

---

## Como funciona

O agente grava SEM perguntar quando detecta:

1. Dono corrige comportamento → `feedback_*.md`
2. Dono valida comportamento não-óbvio → `feedback_*.md`
3. Dono explica quem é → `user_*.md`
4. Dono fala de projeto ativo → `project_*.md`
5. Dono indica onde fica info externa → `reference_*.md`

Atualiza este índice toda vez que cria/edita memória.
