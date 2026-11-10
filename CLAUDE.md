# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

@AGENTS.md

As regras do projeto, os comandos e a estrutura de pastas estão no `AGENTS.md` (importado acima). Aqui fica só o que não está lá.

## Arquitetura

- **Astro 7, 100 % estático.** Não há adaptador de servidor nem `src/pages/api/`: o ADR 0001 (`docs/adr/0001-arquitetura-do-site.md`) prevê acrescentar `@astrojs/node` e os endpoints só no issue #34 (formulários).
- `src/layouts/Base.astro` define o `<html lang="pt-PT">`, o `<head>` (props `title` e `description`), o cabeçalho, o rodapé e o link "Saltar para o conteúdo". Todas as páginas usam `<Base>`.
- A navegação do cabeçalho usa âncoras da página Início (`/#como-funciona`, `/#seguranca`, `/#pedir-demo`), porque as outras páginas ainda não existem.
- `src/styles/global.css` tem os tokens (variáveis CSS) e as classes partilhadas (`.contentor`, `.seccao`, `.botao`…). São provisórios até ao design system (#33). Os estilos de cada página ficam em `<style>` *scoped* no próprio `.astro`.
- Os textos das páginas vêm de `docs/marca.md` (rascunho de marca, #28). O texto final é do #37.

## CI

- `.github/workflows/ci.yml` corre `npm ci`, depois `npm run check` (é o "lint": `astro check`), depois `npm run build` e, no fim, o lychee `--offline` sobre `dist/`.
- Um link interno para uma página que ainda não existe **parte a CI**. Até a página existir, usa âncoras na própria página.
- Não há testes unitários.

## Contexto do repositório

- **Issues ativos: #28–#51** (website). Os #1–#27 estão fechados como fora do âmbito: eram da aplicação, que agora vive em `joaofv7/auditus-app`.
- **PRs:** a descrição tem de ter `Closes #n` em inglês. "Fecha #n" não liga o PR ao issue.
- **PRs empilhados:** o `feat/42-inicio` (página Início) assenta no `feat/base-website`. Faz-se primeiro o merge do branch de base.
- **Mensagem do produto:** a aplicação corre **localmente**, no computador do escritório. O `docs/marca.md` e o `src/pages/index.astro` ainda dizem "servidores dedicados na UE", e isso tem de ser corrigido para "o áudio nunca sai do seu computador". Não afirmar que a lei obriga a correr localmente.
