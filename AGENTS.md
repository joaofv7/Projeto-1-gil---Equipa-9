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
