# inema-mods â€” Kit INEMA de mods do Claude Code

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

[![inema-mods â€” Kit INEMA de mods do Claude Code](guia/assets/banner.jpg)](https://inematds.github.io/inema-mods/guia/)

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/inema-mods/guia/**

**18 mods prontos, em portuguÃªs**, para o Claude Code: proteÃ§Ãµes contra estrago, um painel do contexto, recibo do que foi criado e outros. Cada mod Ã© um acessÃ³rio: vocÃª liga, usa e desliga quando quiser, sem mexer no motor.

> **Mod** Ã© um pedaÃ§o de cÃ³digo que entra no meio do que o Claude Code faz: mostra coisas na tela (faixa, painel, aviso), pergunta antes de uma aÃ§Ã£o perigosa ou troca a aÃ§Ã£o por outra mais segura. NÃ£o gasta crÃ©dito: nenhum mod deste kit chama o modelo, a internet ou serviÃ§o pago.

Testado no **Claude Code 2.1.289** (terminal e app desktop). A API de mods ainda estÃ¡ em teste ("early access") e pode mudar entre versÃµes. Veja [Quando o Claude Code atualizar](#quando-o-claude-code-atualizar).

## Instalar (2 comandos)

```bash
claude plugin marketplace add inematds/inema-mods
claude plugin install freio-de-mao@inema-mods
```

Troque `freio-de-mao` pelo mod que quiser (tabela abaixo). Depois abra uma sessÃ£o nova ou digite `/reload-plugins`.

- SÃ³ neste projeto: acrescente `--scope project`.
- Ver o que um mod faz antes de instalar: `claude plugin details freio-de-mao@inema-mods`, ou leia `mods/freio-de-mao/hooks/register.tsx`.
- Ajustar opÃ§Ãµes (limiares, listas): `/config` dentro do Claude Code.

## Os 18 mods

### ProteÃ§Ã£o

| Mod | O que faz | Comando |
|---|---|---|
| [freio-de-mao](mods/freio-de-mao) | Antes de `rm -rf`, `git reset --hard`, `push --force` e parecidos, mede o estrago **sem apagar** (quantos arquivos, tamanho) e pergunta: Cancelar / Lixeira / Backup e prosseguir / Prosseguir | `/freio` |
| [guarda-colisao](mods/guarda-colisao) | Antes de editar um arquivo que **outra sessÃ£o** mudou, pergunta se pode | `/colisao` |
| [vigia-api](mods/vigia-api) | Pergunta antes de usar serviÃ§o pago (geraÃ§Ã£o de imagem/vÃ­deo, APIs), com autorizaÃ§Ã£o por 1 hora | `/vigia` |
| [modo-gravacao](mods/modo-gravacao) | Para gravar vÃ­deo/live: esconde na tela e-mails, chaves, valores, CPF, telefones | `/gravar on` |
| [faixa-publicacao](mods/faixa-publicacao) | Depois de `git push`, avisa onde foi publicado e que o deploy Ã© automÃ¡tico | â€” |

### Contexto e sessÃ£o

| Mod | O que faz | Comando |
|---|---|---|
| [clima-contexto](mods/clima-contexto) | Faixa com o "tempo" do contexto (limpo, nublado, chuva, tempestade), limites de uso, botÃµes [compactar] e [handoff] | `/contexto` |
| [linha-do-tempo](mods/linha-do-tempo) | Painel turno a turno: modelo, ferramentas, tokens, duraÃ§Ã£o | `/timeline` |
| [roteador-subagente](mods/roteador-subagente) | Faz os subagentes rodarem num modelo menor (poupa a cota) | `/router on` |
| [painel-longrun](mods/painel-longrun) | Acompanha uma execuÃ§Ã£o longa: objetivo, tempo, checklist com % | `/longrun` |

### Produtividade

| Mod | O que faz | Comando |
|---|---|---|
| [recibo-sessao](mods/recibo-sessao) | "O que o Claude criou?" â€” lista de arquivos criados/editados, com [abrir pasta] | `/recibo` |
| [proximos-passos](mods/proximos-passos) | Transforma a lista de prÃ³ximos passos da resposta em botÃµes | `/proximos` |
| [marcador-sessao](mods/marcador-sessao) | Marca um ponto da conversa com resumo, para retomar depois | `/marcar <nome>` |
| [replay-edicoes](mods/replay-edicoes) | Reproduz as ediÃ§Ãµes da sessÃ£o passo a passo, com diff | `/replay` |
| [registrar-falha](mods/registrar-falha) | Depois de erros seguidos, oferece registrar a falha no FALHAS.md | `/falha` |

### Aprender e visual

| Mod | O que faz | Comando |
|---|---|---|
| [tradutor-acoes](mods/tradutor-acoes) | Explica em portuguÃªs simples cada aÃ§Ã£o ("Editando arquivo X"), sem esconder o comando real | `/tradutor` |
| [mapa-calor](mods/mapa-calor) | Mapa das pastas do projeto por quantidade/tamanho | `/mapa` |
| [tema-inema](mods/tema-inema) | RodapÃ© com marca, projeto e hora, para lives | `/tema on` |
| [bichinho](mods/bichinho) | Um bichinho que "come" os arquivos lidos (sÃ³ por diversÃ£o) | `/bichinho on` |

Cada pasta tem um README com comandos, opÃ§Ãµes e **limites honestos** do mod.

## BotÃ£o de pÃ¢nico

```bash
bash scripts/mods-off.sh            # desliga todos os plugins
bash scripts/mods-off.sh --inema    # remove sÃ³ os mods deste kit
bash scripts/mods-doctor.sh         # diz quais mods a sua versÃ£o ainda aceita
```

## Crie o seu prÃ³prio mod

O melhor mod Ã© o feito para o seu jeito de trabalhar. Prompts prontos para copiar e colar em [prompts/](prompts):

0. [Me entreviste e diga quais mods ligar](prompts/00-descubra-seu-mod.md): atÃ© 8 perguntas, nota para cada mod (deste kit e de outros) e o seu top 3 com o primeiro passo.
1. [Descubra os 5 mods que vocÃª precisa](prompts/01-auditoria-sugira-5-mods.md): o Claude lÃª suas Ãºltimas sessÃµes e sugere.
2. [Crie a "previsÃ£o do contexto"](prompts/02-criar-mod-previsao-do-contexto.md).
3. [Crie o "freio de mÃ£o"](prompts/03-criar-mod-freio-de-mao.md).

Para criar: digite `/plugin-authoring` no Claude Code e descreva o mod em portuguÃªs.

## SeguranÃ§a: leia antes de instalar mods de terceiros

Um mod roda com o seu usuÃ¡rio: pode ler arquivos, rodar comandos e acessar a internet. Instale sÃ³ de fontes em que vocÃª confia e leia o `hooks/register.tsx`. Neste kit:

- nenhum mod chama o modelo, a internet ou serviÃ§o pago;
- os mods de proteÃ§Ã£o **reduzem o risco, nÃ£o garantem**: a lista de comandos perigosos nunca Ã© completa, e o modo gravaÃ§Ã£o nÃ£o esconde tudo (veja o README de cada um);
- quando vocÃª nÃ£o estÃ¡ na tela (`claude -p`), os mods de proteÃ§Ã£o **negam** em vez de deixar passar.

## Para quem desenvolve

```bash
scripts/checar-mod.sh mods/<nome>    # claude plugin validate + tsc + claude plugin test
scripts/checar-mod.sh                # todos
python3 scripts/gerar-marketplace.py
```

Regras e pegadinhas da API, aprendidas na prÃ¡tica: [docs/COMO-FAZER-UM-MOD.md](docs/COMO-FAZER-UM-MOD.md).

### Quando o Claude Code atualizar

Rode `bash scripts/mods-doctor.sh`. Se um mod quebrar, desligue com `claude plugin disable <nome>@inema-mods` e veja se o kit tem versÃ£o nova (`claude plugin marketplace update inema-mods`).

---

Feito pelo [INEMA.CLUB](https://inema.club): conteÃºdo aberto e gratuito sobre IA.

---

Projeto adaptado da comunidade INEMA TDS - Marca Arckhe