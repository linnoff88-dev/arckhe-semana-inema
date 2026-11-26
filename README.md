ï»¿# semana-inema ê¢â¬â a semana sem sobrecarga

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![semana-inema](guia/assets/banner.jpg)](https://inematds.github.io/semana-inema/guia/)

**ê°Å¸â¡Â§ê°Å¸â¡Â· [PortuguêÂªs](README.md) êÂ· ê°Å¸â¡Âºê°Å¸â¡Â¸ [English](README.en.md) êÂ· ê°Å¸â¡Âªê°Å¸â¡Â¸ [EspaêÂ±ol](README.es.md)**

## O que êÂ©

O semana-inema êÂ© um kit gratuito para quem cuida de uma comunidade (grupo de Telegram, WhatsApp, turma, lista de e-mail). Toda semana ele lêÂª o que saiu de novo nas suas fontes e monta uma ediêÂ§êÂ£o curta com sete partes: a êÂºnica coisa a fazer, o caminho para cada caso, as vitêÂ³rias dos membros, o que chegou, o que pode ignorar, onde pedir ajuda e quem mais ajudou. Sai em trêÂªs formatos: mensagem de Telegram, e-mail e pêÂ¡gina. Precisa sêÂ³ de Python no computador; nada êÂ© publicado sozinho.

> Sua comunidade nêÂ£o precisa de mais conteêÂºdo. Precisa saber o que fazer.

## ê°Å¸ââ Guia de uso

Guia completo (o mêÂ©todo + passo a passo): **https://inematds.github.io/semana-inema/guia/**

## O processo, do inêÂ­cio ao fim

Quem faz: ê°Å¸Â§Â  o moderador (vocêÂª) êÂ· ê¢Å¡â¢ê¯Â¸Â o script êÂ· ê°Å¸Â¤â um agente (Claude Code ou Codex), opcional.

| # | Passo | Comando / arquivo | Quem |
|---|---|---|---|
| 1 | Ver o exemplo pronto (lêÂª a cêÂ³pia da semana do INEMA que vem no kit) | `python3 semana.py gerar --config config.exemplo.json --de 2026-11-01 --ate 2026-11-08` | ê¢Å¡â¢ê¯Â¸Â |
| 2 | Configurar uma vez: nome, link, plantêÂ£o (o texto da seêÂ§êÂ£o "Travou?") e a sua tabela de publicados | `cp config.modelo.json config.json`, depois `config.json` e `publicados.md` | ê°Å¸Â§Â  |
| 3 | Durante a semana, anotar vitêÂ³rias e quem ajudou (com licenêÂ§a das pessoas) | `vitorias.md`, `ajudantes.md` | ê°Å¸Â§Â  |
| 4 | Juntar o que chegou na semana e montar o rascunho | `python3 semana.py rascunho` ê¢â â `saida/<data>/rascunho.md` | ê¢Å¡â¢ê¯Â¸Â |
| 5 | Escolher a êÂºnica coisa, a tabela "seu caso ê¢â â seu caminho" e o "pode ignorar" | colar `prompts/escolher-a-unica-coisa.md` ê¢â â escreve `edicao.md` | ê°Å¸Â¤â (ou ê°Å¸Â§Â  êÂ  mêÂ£o) |
| 6 | Ler e ajustar a escolha (a linha `semana:` tem que ser o êÂºltimo dia da semana; ediêÂ§êÂ£o de outra semana êÂ© recusada) | `edicao.md` | ê°Å¸Â§Â  |
| 7 | Gerar os trêÂªs formatos | `python3 semana.py gerar` ê¢â â `telegram.md` (+ `telegram-2.md`ê¢â¬Â¦), `email.html`, `pagina.html` | ê¢Å¡â¢ê¯Â¸Â |
| 8 | Conferir e publicar (o kit nêÂ£o envia nada) | colar no grupo, no e-mail, no site | ê°Å¸Â§Â  |

Para uma semana que nêÂ£o termina hoje, passe as datas nos passos 4 e 7: `--ate AAAA-MM-DD` (êÂºltimo dia) e, se quiser, `--de AAAA-MM-DD`. Sem `--de`, a janela êÂ© de 7 dias terminando no `--ate`.

## ComeêÂ§ar

```bash
git clone https://github.com/inematds/semana-inema.git
cd semana-inema
python3 -m unittest discover -s tests
python3 semana.py gerar --config config.exemplo.json --de 2026-11-01 --ate 2026-11-08
```

Depois, para a sua comunidade: crie o `publicados.md`, copie o modelo genêÂ©rico por cima do config (`cp config.modelo.json config.json`; no Windows, `copy`), troque nele o nome, o link e o plantêÂ£o, apague os exemplos de `vitorias.md`/`ajudantes.md` e rode:

```bash
python3 semana.py rascunho
python3 semana.py gerar
```

Formato do `publicados.md` (uma linha por publicaêÂ§êÂ£o; sem "publicado" fica de fora):

```markdown
| Tema | Data | Estado |
|---|---|---|
| Aula: o primeiro agente | 05/11/2026 | publicado 05/11/2026 ê¢â¬â https://exemplo.com/aula |
| Guia do backup | 06/11/2026 | em produêÂ§êÂ£o |
```

SêÂ³ biblioteca padrêÂ£o do Python 3 (nada de `pip install`). No Windows, troque `python3` por `py`.

## As sete seêÂ§êÂµes

1. **A êÂºnica coisa desta semana** ê¢â¬â uma tarefa que termina com 1 resultado funcionando (nêÂ£o "assisti o vêÂ­deo").
2. **Seu caso ê¢â â seu caminho** ê¢â¬â tabela "usa X ê¢â â veja Y".
3. **VitêÂ³rias da comunidade** ê¢â¬â de `vitorias.md`: `- Nome ê¢â¬â o que fez ê¢â¬â link`.
4. **O que chegou** ê¢â¬â lido das fontes, sêÂ³ o que caiu na janela da semana.
5. **Pode ignorar** ê¢â¬â 2 a 4 novidades que podem esperar, com o motivo.
6. **Travou?** ê¢â¬â onde e como pedir ajuda (texto do plantêÂ£o no `config.json`).
7. **Quem mais ajudou** ê¢â¬â ranking manual de `ajudantes.md` (opcional; vazio aparece como vazio).

## Fontes de "O que chegou" (`config.json` ê¢â¬Âº `fontes`)

| tipo | O que lêÂª | Campos |
|---|---|---|
| `tabela_md` | Tabela Markdown de publicaêÂ§êÂµes. Entra a linha cujo estado comeêÂ§a com a palavra de `so_com` (no INEMA, "publicad", que vale para publicado e publicada; em inglêÂªs, "published"); a data êÂ© a escrita depois dessa palavra (dd/mm ou dd/mm/aaaa) ou, se faltar, a da coluna de data. Linhas sem data ficam de fora e sêÂ£o contadas. | `caminho`, `coluna_titulo`, `coluna_data`, `coluna_estado`, `so_com`, `padrao_id_youtube` (opcional) |
| `git_log` | Commits dos repositêÂ³rios listados, na janela da semana (sem merges). | `repos`, `ignorar_prefixos`, `link_repo` |
| `feed` | Arquivo salvo no disco: JSON (`titulo`/`data`/`link`) ou RSS/Atom. URL nêÂ£o êÂ© lida (o kit nêÂ£o usa rede). | `caminho` |

Cada fonte liga e desliga com `"ativo": true/false`.

## Telegram: limite de 4.096

O texto do Telegram êÂ© contado como o Telegram conta (unidades UTF-16: emoji vale 2). Se passar de 4.096, o kit divide em `telegram.md`, `telegram-2.md`ê¢â¬Â¦ cortando de preferêÂªncia no inêÂ­cio de uma seêÂ§êÂ£o. O teste `tests/test_semana.py` confere que nenhuma parte passa do limite e que nada se perde.

## Exemplo real: a semana do INEMA (01 a 08/11/2026)

Em [`exemplos/2026-11-08/`](exemplos/2026-11-08/): `publicados.md` (cêÂ³pia limpa da semana), `rascunho.md`, `telegram.md`, `email.html`, `pagina.html` e prints em 1440 px e 390 px. O kit vem configurado para o INEMA (lêÂª a tabela de produêÂ§êÂµes de vêÂ­deo do INEMA); troque o `config.json` para a sua comunidade.

- Tabela lida (08/11/2026): 90 linhas, 50 publicadas com data, **26 na semana**.
- A êÂºnica coisa: *Responda as 6 perguntas da Escada do NegêÂ³cio com IA e escolha UM negêÂ³cio para comeêÂ§ar.*
- Telegram: 3.671 caracteres, 1 mensagem.
- VitêÂ³rias do exemplo: entregas do prêÂ³prio INEMA, marcadas "(exemplo)". Ajudantes: vazio (o kit nêÂ£o inventa nomes).

Comandos usados:

```bash
python3 semana.py rascunho --de 2026-11-01 --ate 2026-11-08 --saida exemplos
python3 semana.py gerar    --de 2026-11-01 --ate 2026-11-08 --saida exemplos
```

## Arquivos

| Arquivo | Para quêÂª |
|---|---|
| `semana.py` | o script (rascunho e gerar) |
| `config.json` | comunidade, link, plantêÂ£o, fontes (vem com o INEMA, que lêÂª a tabela interna de produêÂ§êÂµes) |
| `config.exemplo.json` | roda o exemplo em qualquer clone (lêÂª `exemplos/2026-11-08/publicados.md`) |
| `config.modelo.json` | modelo genêÂ©rico para a sua comunidade (lêÂª `publicados.md`); copie por cima do `config.json` |
| `vitorias.md`, `ajudantes.md` | o que o moderador anota na semana |
| `edicao.md` | a escolha da semana (êÂºnica coisa, seu caso, pode ignorar); a que vem no kit êÂ© o exemplo do INEMA |
| `prompts/escolher-a-unica-coisa.md` | pedido pronto para o Claude Code ou o Codex |
| `tests/` | testes sem rede (`python3 -m unittest discover -s tests`) |
| `exemplos/` | a ediêÂ§êÂ£o real do INEMA |
| `guia/` | pêÂ¡gina de apresentaêÂ§êÂ£o e guia (PT/EN/ES) |

## LicenêÂ§a

MIT. Feito pelo [INEMA.CLUB](https://inema.club).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>