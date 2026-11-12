# ADR 0001 — Arquitetura do site

- **Estado:** proposto. É aprovado pelo Pedro e pelo Gonçalo na revisão do PR.
- **Issue:** #30
- **Data:** 2026-11-10

## Contexto

O site é institucional: apresenta o Auditus e recebe pedidos de demonstração. Não tem contas nem área de cliente.
Tem de ser rápido (Lighthouse ≥ 90), acessível e coerente com a promessa do produto: nenhum dado sai da UE
e não se carregam recursos de terceiros sem justificação.

## Decisões

### 1. Framework: Astro, páginas estáticas

- As páginas são geradas no build como HTML estático, com zero JavaScript por omissão.
- Os endpoints dos formulários (pedir demo, newsletter, agendamento) ficam no mesmo projeto, em `src/pages/api/`,
  marcados com `export const prerender = false`.
- Para isso será acrescentado o adaptador `@astrojs/node` (modo *standalone*) no #34. Até lá o site é 100 % estático.

**Porquê:** é o que dá melhor performance a um site de conteúdo, tem MDX e coleções de conteúdo de série
e permite ter os formulários sem um segundo serviço. Next.js e Nuxt trariam um framework de UI inteiro para páginas
que são quase só texto.

### 2. Estilos e componentes

- Componentes `.astro` com o CSS isolado (*scoped*) que o Astro já oferece.
- Os *tokens* do design system (cores, tipografia, espaçamentos) são variáveis CSS num ficheiro global (#33).
- Sem framework de UI. As partes interativas (demo da página Produto, calculadora de preços) usam `<script>` simples.
  Se a demo ficar complexa, acrescenta-se Preact apenas nessa ilha, por decisão registada aqui.
- Fontes servidas a partir de `public/`, nunca de CDNs externos.

**Porquê:** zero dependências extra e nenhum JavaScript desnecessário. Tailwind é uma alternativa válida
se o Pedro preferir; essa decisão fica fechada na revisão deste ADR.

### 3. Conteúdo: ficheiros no repositório

- Coleções de conteúdo do Astro em `src/content/`: blog em MDX, FAQ e planos em ficheiros de dados (YAML/JSON).
- Publicar = abrir PR. Rascunhos têm `draft: true` e são excluídos do build de produção.
- Implementado no #36.

**Porquê:** não há mais um serviço para manter nem dados guardados fora da UE. Um CMS *headless* (ex.: Directus
alojado na UE) só se justifica se alguém sem acesso ao Git tiver de publicar com frequência.

### 4. Formulários e dados pessoais

- Validação sempre no servidor. Proteção anti-spam com *honeypot* e limitação de pedidos, sem CAPTCHAs de terceiros.
- Envio de email por SMTP de um fornecedor com servidores na UE (escolha no #34).
- Armazenamento dos leads numa base de dados na UE, encriptada em repouso (escolha no #39).

### 5. Alojamento e ambientes

- **Por decidir no #32.** Requisitos: região na UE, Node.js 22+, deploy automático a partir do `main`.
- Ambientes: local (`npm run dev`), pré-visualização por PR (#32) e produção.
- A CI (GitHub Actions) corre `astro check`, o build e a verificação de links internos em cada PR.

### 6. Língua

- Só PT-PT (`<html lang="pt-PT">`). Não se instala i18n até haver uma segunda língua.

### 7. Estrutura de pastas

```
src/pages/        páginas; src/pages/api/ = endpoints
src/components/   componentes
src/layouts/      layouts de página
src/content/      blog, FAQ, planos
src/styles/       tokens e estilos globais
public/           imagens, fontes, áudio da demo
docs/adr/         decisões de arquitetura
```

## Consequências

- O Pedro pode começar o design system e as páginas sem esperar pelo backend.
- O Miguel acrescenta o adaptador Node e os endpoints quando chegar ao #34. Até lá, o site pode ser alojado como estático.
- Qualquer serviço novo fora da UE tem de ser justificado num novo ADR.
