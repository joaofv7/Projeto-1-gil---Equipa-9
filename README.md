# Auditus — website

Site institucional do Auditus: apresenta o produto e recebe pedidos de demonstração de advogados e solicitadores.
Feito em [Astro](https://docs.astro.build). As decisões técnicas estão em [docs/adr/0001-arquitetura-do-site.md](docs/adr/0001-arquitetura-do-site.md).

## Arrancar localmente

Precisas de Node.js 22.23 ou mais recente e de Git.

```bash
git clone https://github.com/joaofv7/Projeto-1-gil---Equipa-9.git
cd Projeto-1-gil---Equipa-9
npm ci
npm run dev
```

O site abre em http://localhost:4321.

| Comando | O que faz |
|---|---|
| `npm run dev` | Servidor de desenvolvimento com recarregamento automático |
| `npm run check` | Verifica tipos e erros nos ficheiros `.astro` (é o "lint" da CI) |
| `npm run build` | Gera o site final em `dist/` |
| `npm run preview` | Serve o `dist/` localmente para testar o build |

## Estrutura

```
src/pages/        páginas (cada ficheiro = um URL); src/pages/api/ = endpoints dos formulários
src/components/   componentes reutilizáveis (design system)
src/content/      conteúdo editável: blog, FAQ, planos
public/           ficheiros servidos tal como estão (imagens, fontes, áudio da demo)
docs/adr/         decisões de arquitetura
```

## Como trabalhamos

- `main` está sempre pronto a publicar. Ninguém faz push direto para `main`.
- Cada issue tem um branch: `feat/<nº>-descricao`, `fix/<nº>-descricao` ou `docs/<nº>-descricao`.
- Abre um PR com `Fecha #<nº>`. A CI tem de passar e o dono da pasta (ver `.github/CODEOWNERS`) tem de aprovar.
- Faz merge com *squash*.

## Segredos

- Nunca ponhas segredos no Git. Copia `.env.example` para `.env` e preenche localmente.
- Na CI e em produção, os segredos ficam nas definições do GitHub/fornecedor de alojamento.

## Alojamento

Por decidir no #32 (fornecedor e região na UE). O site corre em qualquer servidor com Node.js.
