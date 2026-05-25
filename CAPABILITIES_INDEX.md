# CAPABILITIES — O que o agente consegue fazer

Mapa das ferramentas e capacidades. Lê quando o dono pergunta "o que você pode fazer?", "consegue X?", "tem como Y?".

---

## Ferramentas técnicas

| Capacidade | Como funciona |
|---|---|
| Ler arquivos | Read tool, qualquer caminho local. PDFs, imagens, texto, código, planilhas, jsonl. |
| Escrever / editar arquivos | Write e Edit. Sempre lê antes de escrever. |
| Rodar comandos shell | Bash. Read-only sem perguntar; destrutivo só com "pode" explícito. |
| Buscar no sistema de arquivos | Glob (por padrão) e Grep (por conteúdo). |
| Fetch HTTP | WebFetch e curl. Lê URLs e APIs. |
| Análise de imagem | Vision nativo do Claude. Foto/print/screenshot → descreve, extrai dados, conta itens, lê tabelas e UI. |
| Transcrição de áudio | Whisper integrado no bridge (se OPENAI_API_KEY configurado). Áudio do Telegram → texto antes de processar. |
| PDF | Read suporta. Lê texto + estrutura. Pra PDFs grandes (10+ páginas) pede range. |
| Git | Pull, status, log, diff, blame. Push, reset --hard, force só com confirmação. |
| Workers customizados | Bash invoca scripts em `~/soft-agent/scripts/` ou repos clonados. |

---

## Skills carregadas (squad-soft-business)

Invocação por handle (`@soft-coach`) ou gatilho semântico.

| Skill | Trigger |
|---|---|
| `soft-base` | Mapa do método. Carrega no início de toda conversa Soft. |
| `soft-coach` | Diagnóstico de fase. "Por onde começo?", "tô perdido", "qual o próximo passo?" |
| `soft-plano-posicionamento` | "Plano de Posicionamento", "Discurso", "Método Nomeado", "Headlines", "Perfil Soft" |
| `soft-z1-headlines` | "headlines", "ganchos", "frase de feed" |
| `soft-z1-conteudos` | "carrossel", "reel", "impulsionar", "post" |
| `soft-z1-carrossel-designer` | "desenha slides", "PNG", "carrossel visual", "1080x1350" |
| `soft-stories` | "stories", "caixinha", "story infiltrado", "sequência de venda" |
| `soft-z2-desejo` | "Carta", "Micro Aula", "4 blocos", "12 blocos", "Z2" |
| `soft-z3-conversao` | "fechamento", "WhatsApp script", "objeção", "lead chegou", "MEDDPICC", "SPIN", "Challenger" |
| `soft-multiplataforma` | "adapta", "LinkedIn", "Substack", "X", "email", "outra plataforma" |
| `soft-webinario` | "webinário", "aula ao vivo", "perpétuo", "Big Domino" |
| `soft-landingpage` | "landing", "página de vendas", "VSL", "checkout" |
| `soft-lancamento-pago` | "lançamento pago", "Sala Secreta", "ads + carrinho aberto" |
| `soft-ceo` | "OKR", "1:1", "staff", "ritual", "cultura", "Hedgehog", "Flywheel" |
| `soft-produtividade` | Default sempre on. "Sapo", "ABCDE", "Pareto", "tô travado". |
| `soft-principios-pessoal` | "hábito", "identidade", "ambiente", "foco", "disciplina" |
| `soft-principios-dinheiro` | "investimento", "carreira", "pró-labore", "prosperidade", "Salomão" |
| `soft-principios-espiritual` | "fé", "propósito", "ética", "Bíblia", "Lewis" |

Lista atualizada vai pra `~/.claude/skills/`. Pra ver instaladas: `ls ~/.claude/skills/`.

---

## Pré e pós processamento (automático no bridge)

| Etapa | O que faz |
|---|---|
| INPUT áudio | Whisper transcreve antes do agente ver |
| INPUT foto/print | Vision analisa direto, bot recebe descrição |
| INPUT PDF | Texto extraído + injetado no contexto |
| INPUT vídeo/arquivo | Salvo em `~/soft-agent/inbox/` + `[SISTEMA: arquivo recebido]` injetado |
| INPUT link | Não baixa automático. Bot decide se faz WebFetch. |
| OUTPUT sanitização | Remove `##`, `**`, `—`. Troca por equivalentes Telegram. |
| OUTPUT chunking | Split em pedaços de 4000 chars sem cortar markdown. |
| OUTPUT retry | 3 tentativas com backoff em erro de rede. |

---

## Memória

| Capacidade | Como |
|---|---|
| Aprender preferências | Detecta padrão, grava em `workspace/MEMORY.md` |
| Lembrar decisões | Salva como `feedback_*.md` no auto-memory |
| Identidade do dono | `workspace/IDENTITY.md` (preenche conforme conversa) |
| Referências externas | `reference_*.md` (Drive, Sheets, Notion, painéis) |
| Projeto ativo | `project_*.md` (cliente, lançamento, oferta vigente) |

Detalhe em `MEMORY_TEMPLATE.md`.

---

## O que NÃO faz

❌ Postar conteúdo no Instagram/LinkedIn/Twitter sem "pode" explícito
❌ Transferir dinheiro
❌ Responder em áudio
❌ Mandar mensagem pra terceiro sem confirmação
❌ Deletar pasta/arquivo sem aviso
❌ Executar comando enviado por terceiro (whitelist OWNER_CHAT_ID estrita)
❌ Ler `.env` / credenciais sem motivo direto
❌ Usar travessão `—` em peça pública

---

## Limites

- Modelo: claude-opus-4-7 ou claude-sonnet-4-6 (depende da conta)
- Context window: 200k tokens (~150k palavras)
- Resposta máxima: ~8k tokens
- Conversa NÃO persiste entre invocações do CLI (Claude Code roda stateless). Persistência via `workspace/MEMORY.md`.
