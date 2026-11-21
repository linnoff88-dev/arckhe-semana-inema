# semana-inema â€” a semana sem sobrecarga

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


[![semana-inema](guia/assets/banner.jpg)](https://inematds.github.io/semana-inema/guia/)

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

## O que Ã©

O semana-inema Ã© um kit gratuito para quem cuida de uma comunidade (grupo de Telegram, WhatsApp, turma, lista de e-mail). Toda semana ele lÃª o que saiu de novo nas suas fontes e monta uma ediÃ§Ã£o curta com sete partes: a Ãºnica coisa a fazer, o caminho para cada caso, as vitÃ³rias dos membros, o que chegou, o que pode ignorar, onde pedir ajuda e quem mais ajudou. Sai em trÃªs formatos: mensagem de Telegram, e-mail e pÃ¡gina. Precisa sÃ³ de Python no computador; nada Ã© publicado sozinho.

> Sua comunidade nÃ£o precisa de mais conteÃºdo. Precisa saber o que fazer.

## ðŸ“– Guia de uso

Guia completo (o mÃ©todo + passo a passo): **https://inematds.github.io/semana-inema/guia/**

## O processo, do inÃ­cio ao fim

Quem faz: ðŸ§  o moderador (vocÃª) Â· âš™ï¸ o script Â· ðŸ¤– um agente (Claude Code ou Codex), opcional.

| # | Passo | Comando / arquivo | Quem |
|---|---|---|---|
| 1 | Ver o exemplo pronto (lÃª a cÃ³pia da semana do INEMA que vem no kit) | `python3 semana.py gerar --config config.exemplo.json --de 2026-11-01 --ate 2026-11-08` | âš™ï¸ |
| 2 | Configurar uma vez: nome, link, plantÃ£o (o texto da seÃ§Ã£o "Travou?") e a sua tabela de publicados | `cp config.modelo.json config.json`, depois `config.json` e `publicados.md` | ðŸ§  |
| 3 | Durante a semana, anotar vitÃ³rias e quem ajudou (com licenÃ§a das pessoas) | `vitorias.md`, `ajudantes.md` | ðŸ§  |
| 4 | Juntar o que chegou na semana e montar o rascunho | `python3 semana.py rascunho` â†’ `saida/<data>/rascunho.md` | âš™ï¸ |
| 5 | Escolher a Ãºnica coisa, a tabela "seu caso â†’ seu caminho" e o "pode ignorar" | colar `prompts/escolher-a-unica-coisa.md` â†’ escreve `edicao.md` | ðŸ¤– (ou ðŸ§  Ã  mÃ£o) |
| 6 | Ler e ajustar a escolha (a linha `semana:` tem que ser o Ãºltimo dia da semana; ediÃ§Ã£o de outra semana Ã© recusada) | `edicao.md` | ðŸ§  |
| 7 | Gerar os trÃªs formatos | `python3 semana.py gerar` â†’ `telegram.md` (+ `telegram-2.md`â€¦), `email.html`, `pagina.html` | âš™ï¸ |
| 8 | Conferir e publicar (o kit nÃ£o envia nada) | colar no grupo, no e-mail, no site | ðŸ§  |

Para uma semana que nÃ£o termina hoje, passe as datas nos passos 4 e 7: `--ate AAAA-MM-DD` (Ãºltimo dia) e, se quiser, `--de AAAA-MM-DD`. Sem `--de`, a janela Ã© de 7 dias terminando no `--ate`.

## ComeÃ§ar

```bash
git clone https://github.com/inematds/semana-inema.git
cd semana-inema
python3 -m unittest discover -s tests
python3 semana.py gerar --config config.exemplo.json --de 2026-11-01 --ate 2026-11-08
```

Depois, para a sua comunidade: crie o `publicados.md`, copie o modelo genÃ©rico por cima do config (`cp config.modelo.json config.json`; no Windows, `copy`), troque nele o nome, o link e o plantÃ£o, apague os exemplos de `vitorias.md`/`ajudantes.md` e rode:

```bash
python3 semana.py rascunho
python3 semana.py gerar
```

Formato do `publicados.md` (uma linha por publicaÃ§Ã£o; sem "publicado" fica de fora):

```markdown
| Tema | Data | Estado |
|---|---|---|
| Aula: o primeiro agente | 05/11/2026 | publicado 05/11/2026 â€” https://exemplo.com/aula |
| Guia do backup | 06/11/2026 | em produÃ§Ã£o |
```

SÃ³ biblioteca padrÃ£o do Python 3 (nada de `pip install`). No Windows, troque `python3` por `py`.

## As sete seÃ§Ãµes

1. **A Ãºnica coisa desta semana** â€” uma tarefa que termina com 1 resultado funcionando (nÃ£o "assisti o vÃ­deo").
2. **Seu caso â†’ seu caminho** â€” tabela "usa X â†’ veja Y".
3. **VitÃ³rias da comunidade** â€” de `vitorias.md`: `- Nome â€” o que fez â€” link`.
4. **O que chegou** â€” lido das fontes, sÃ³ o que caiu na janela da semana.
5. **Pode ignorar** â€” 2 a 4 novidades que podem esperar, com o motivo.
6. **Travou?** â€” onde e como pedir ajuda (texto do plantÃ£o no `config.json`).
7. **Quem mais ajudou** â€” ranking manual de `ajudantes.md` (opcional; vazio aparece como vazio).

## Fontes de "O que chegou" (`config.json` â€º `fontes`)

| tipo | O que lÃª | Campos |
|---|---|---|
| `tabela_md` | Tabela Markdown de publicaÃ§Ãµes. Entra a linha cujo estado comeÃ§a com a palavra de `so_com` (no INEMA, "publicad", que vale para publicado e publicada; em inglÃªs, "published"); a data Ã© a escrita depois dessa palavra (dd/mm ou dd/mm/aaaa) ou, se faltar, a da coluna de data. Linhas sem data ficam de fora e sÃ£o contadas. | `caminho`, `coluna_titulo`, `coluna_data`, `coluna_estado`, `so_com`, `padrao_id_youtube` (opcional) |
| `git_log` | Commits dos repositÃ³rios listados, na janela da semana (sem merges). | `repos`, `ignorar_prefixos`, `link_repo` |
| `feed` | Arquivo salvo no disco: JSON (`titulo`/`data`/`link`) ou RSS/Atom. URL nÃ£o Ã© lida (o kit nÃ£o usa rede). | `caminho` |

Cada fonte liga e desliga com `"ativo": true/false`.

## Telegram: limite de 4.096

O texto do Telegram Ã© contado como o Telegram conta (unidades UTF-16: emoji vale 2). Se passar de 4.096, o kit divide em `telegram.md`, `telegram-2.md`â€¦ cortando de preferÃªncia no inÃ­cio de uma seÃ§Ã£o. O teste `tests/test_semana.py` confere que nenhuma parte passa do limite e que nada se perde.

## Exemplo real: a semana do INEMA (01 a 08/11/2026)

Em [`exemplos/2026-11-08/`](exemplos/2026-11-08/): `publicados.md` (cÃ³pia limpa da semana), `rascunho.md`, `telegram.md`, `email.html`, `pagina.html` e prints em 1440 px e 390 px. O kit vem configurado para o INEMA (lÃª a tabela de produÃ§Ãµes de vÃ­deo do INEMA); troque o `config.json` para a sua comunidade.

- Tabela lida (08/11/2026): 90 linhas, 50 publicadas com data, **26 na semana**.
- A Ãºnica coisa: *Responda as 6 perguntas da Escada do NegÃ³cio com IA e escolha UM negÃ³cio para comeÃ§ar.*
- Telegram: 3.671 caracteres, 1 mensagem.
- VitÃ³rias do exemplo: entregas do prÃ³prio INEMA, marcadas "(exemplo)". Ajudantes: vazio (o kit nÃ£o inventa nomes).

Comandos usados:

```bash
python3 semana.py rascunho --de 2026-11-01 --ate 2026-11-08 --saida exemplos
python3 semana.py gerar    --de 2026-11-01 --ate 2026-11-08 --saida exemplos
```

## Arquivos

| Arquivo | Para quÃª |
|---|---|
| `semana.py` | o script (rascunho e gerar) |
| `config.json` | comunidade, link, plantÃ£o, fontes (vem com o INEMA, que lÃª a tabela interna de produÃ§Ãµes) |
| `config.exemplo.json` | roda o exemplo em qualquer clone (lÃª `exemplos/2026-11-08/publicados.md`) |
| `config.modelo.json` | modelo genÃ©rico para a sua comunidade (lÃª `publicados.md`); copie por cima do `config.json` |
| `vitorias.md`, `ajudantes.md` | o que o moderador anota na semana |
| `edicao.md` | a escolha da semana (Ãºnica coisa, seu caso, pode ignorar); a que vem no kit Ã© o exemplo do INEMA |
| `prompts/escolher-a-unica-coisa.md` | pedido pronto para o Claude Code ou o Codex |
| `tests/` | testes sem rede (`python3 -m unittest discover -s tests`) |
| `exemplos/` | a ediÃ§Ã£o real do INEMA |
| `guia/` | pÃ¡gina de apresentaÃ§Ã£o e guia (PT/EN/ES) |

## LicenÃ§a

MIT. Feito pelo [INEMA.CLUB](https://inema.club).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>