# AGENTS.md — regras para agentes de IA neste repositório

Lê este ficheiro inteiro antes de mexer em qualquer coisa. Vale para qualquer agente (Claude, Antigravity, Copilot, Cursor, Codex…).

## O que é este projeto

- **Website institucional do Auditus**: apresenta o produto e recebe pedidos de demonstração de advogados e solicitadores portugueses.
- **Não é a aplicação do produto.** Não há contas, login, upload de áudio nem transcrição real neste repositório.
- O Auditus (o produto) transcreve audiências judiciais com identificação de locutores, processado só em servidores na UE (RGPD, sigilo profissional). O site tem de **provar confidencialidade** e converter visitas em pedidos de demo.
- Contexto completo do produto: `Auditus-AI-Legal-Transcription-Diarization-Engine.md` (PRD, fora deste repositório) e os issues #28–#51.

## Stack e comandos

- [Astro](https://docs.astro.build) 7, páginas estáticas, TypeScript estrito. Node.js ≥ 22.23.
- Decisões de arquitetura: `docs/adr/`. **Lê o ADR 0001 antes de propor tecnologia.**

| Comando | Para quê |
|---|---|
| `npm ci` | Instalar dependências |
| `npm run dev` | Servidor local em http://localhost:4321 |
| `npm run check` | Lint/tipos — tem de dar 0 erros antes de qualquer commit |
| `npm run build` | Build de produção em `dist/` — tem de passar |
| `npm run preview` | Servir o build localmente |

Se precisares de deixar o servidor a correr enquanto trabalhas, usa `npx astro dev --background` e gere-o com `npx astro dev stop | status | logs`.

## Estrutura

```
src/pages/        páginas (ficheiro = URL); src/pages/api/ = endpoints dos formulários
src/components/   componentes do design system
src/layouts/      layouts de página
src/content/      blog (MDX), FAQ e planos (YAML/JSON)
src/styles/       tokens (variáveis CSS) e estilos globais
public/           imagens, fontes, áudio da demo
docs/adr/         decisões de arquitetura
```

## Arquitetura e armadilhas

### Arquitetura
- **100 % estático.** Não há adaptador de servidor nem `src/pages/api/`. O ADR 0001 prevê acrescentar o `@astrojs/node` e os endpoints só no #34 (formulários).
- **Layout comum** (a partir da página Início, PR #54):
  - `src/layouts/Base.astro` define o `<html lang="pt-PT">`, o `<head>` (props `title` e `description`), o cabeçalho, o rodapé e o link "Saltar para o conteúdo". Todas as páginas usam `<Base>`.
  - A navegação do cabeçalho usa âncoras da página Início (`/#como-funciona`, `/#seguranca`, `/#pedir-demo`), porque as outras páginas ainda não existem.
  - `src/styles/global.css` tem os tokens (variáveis CSS) e as classes partilhadas (`.contentor`, `.seccao`, `.botao`…). São provisórios até ao design system (#33). Os estilos de cada página ficam em `<style>` *scoped* no próprio `.astro`.
- Os textos das páginas vêm de `docs/marca.md` (rascunho de marca, #28). O texto final é do #37.

### CI
- `.github/workflows/ci.yml` corre `npm ci`, depois `npm run check` (`astro check`), depois `npm run build` e, no fim, o lychee `--offline` sobre `dist/`.
- **Um link interno para uma página que ainda não existe parte a CI.** Até a página existir, usa âncoras na própria página.
- Não há testes unitários.

### Contexto do repositório
- **Issues ativos: #28–#51** (website). Os #1–#27 estão fechados como fora do âmbito: eram da aplicação, que agora vive em `joaofv7/auditus-app`.
- **PRs empilhados:** o `feat/42-inicio` (página Início) assenta no `feat/base-website`. Faz-se primeiro o merge do branch de base.
- **Mensagem do produto:** a aplicação corre **localmente**, no computador do escritório. O `docs/marca.md` e a página Início ainda dizem "servidores dedicados na UE", e isso tem de passar a "o áudio nunca sai do seu computador". Não afirmar que a lei obriga a correr localmente.

## Regras obrigatórias

### Privacidade e RGPD (a promessa central do produto)
- **Nada de recursos de terceiros**: sem CDNs, Google Fonts, scripts de analytics, embeds, CAPTCHAs ou pixels. Fontes e imagens vão para `public/`.
- **Nenhum serviço fora da UE** (email, base de dados, alojamento, agendamento, analytics). Se for mesmo preciso, pára e propõe um novo ADR.
- **Nunca** ponhas segredos, tokens ou dados pessoais reais no código. Segredos vão para `.env` (ignorado pelo Git); documenta a variável em `.env.example` com valor de exemplo.
- Formulários: validação no servidor, consentimento RGPD explícito, anti-spam sem cookies de terceiros.
- A demo da página Produto usa **só dados fictícios**. O WhisperX corre apenas localmente, offline, para gerar o JSON de exemplo; nunca é chamado pelo site.

### Texto e conteúdo
- Todo o texto visível é **português de Portugal** (PT-PT). Nunca pt-BR: "ecrã" e não "tela", "telemóvel" e não "celular", "utilizador" e não "usuário", "ficheiro" e não "arquivo", "equipa" e não "time".
- Tom sóbrio e rigoroso, para o setor jurídico.
- **Não inventes números nem promessas.** Os únicos objetivos de desempenho são os do PRD: taxa de erro (WER) abaixo de 9 % e processamento em menos de 1/3 da duração do áudio, apresentados como objetivos e não como garantias.
- `<html lang="pt-PT">` em todas as páginas.

### Qualidade
- Zero JavaScript por omissão; `<script>` só onde há interação real. Sem frameworks de UI (React, Vue…) sem ADR.
- Acessibilidade WCAG 2.2 AA: HTML semântico, navegação por teclado, foco visível, contraste, texto alternativo.
- Objetivo Lighthouse ≥ 90 em todas as categorias.
- Não acrescentes dependências npm para coisas que se fazem em poucas linhas ou que o Astro já faz.

## Como trabalhar

- Cada alteração corresponde a um issue (#28–#51). Lê o issue e respeita os critérios de aceitação e as dependências ("Depende de").
- Branch por issue: `feat/<nº>-descricao`, `fix/<nº>-descricao` ou `docs/<nº>-descricao`.
- **Nunca faças push para `main`** nem force-push. Abre PR com `Closes #<nº>` (em inglês, senão o GitHub não fecha o issue) e preenche o template.
- **Nunca apagues branches**, nem depois do merge: o professor avalia o trabalho de cada issue pelos branches. Faz merge sem `--delete-branch` e não ligues a opção "Automatically delete head branches" do GitHub.
- Antes de commit: `npm run check` e `npm run build` têm de passar.
- Commits e PRs em português, curtos e no imperativo ("Adiciona página Preços").
- Decisões técnicas novas ou contrárias ao ADR 0001 → novo ficheiro `docs/adr/000N-titulo.md`, não uma alteração silenciosa.

## Equipa e responsabilidades

| Pessoa | GitHub | Área |
|---|---|---|
| Gonçalo | `joaofv7` | Marca, conteúdo, infraestrutura, legal, SEO, lançamento |
| Miguel | `NumerosMikas` | Backend: formulários, conteúdo, segurança, dados dos leads |
| Pedro | `pedroformosinho2006-lab` | Frontend: design system e páginas |

Os revisores obrigatórios por pasta estão em `.github/CODEOWNERS`.

## Documentação do Astro

- [Rotas, páginas e middleware](https://docs.astro.build/en/guides/routing/)
- [Componentes Astro](https://docs.astro.build/en/basics/astro-components/)
- [Coleções de conteúdo](https://docs.astro.build/en/guides/content-collections/)
- [Estilos](https://docs.astro.build/en/guides/styling/)
- [Endpoints](https://docs.astro.build/en/guides/endpoints/)
