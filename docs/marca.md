# Marca, posicionamento e mensagens-chave

- **Issue:** #28
- **Estado:** rascunho para aprovação do Gonçalo, do Miguel e do Pedro
- **Fonte:** PRD do Auditus e pesquisa pública a alternativas (novembro de 2026)

Este documento é a referência para o design (#31, #33), os textos (#37), as páginas legais (#38) e o SEO (#47).
Se uma página disser algo que não está aqui, ou que contradiz o que está aqui, corrige-se a página ou atualiza-se este documento.

---

## 1. Em uma frase

**O Auditus transforma horas de gravação de audiências em texto pesquisável, separado por quem fala, em minutos e sem que o áudio saia da Europa.**

## 2. Público-alvo

| Perfil | O que lhe dói | O que valoriza | Principal objeção |
|---|---|---|---|
| **Advogado de contencioso** (utilizador principal) | Ouvir horas de gravação para encontrar uma frase de uma testemunha | Encontrar a citação exata e o minuto, rapidamente | "A IA vai errar e eu não vou dar por isso" |
| **Solicitador** | Inquirições e diligências longas, sem tempo para as transcrever | Texto separado por interveniente, pronto a usar | "É caro para o volume que tenho" |
| **Assistente jurídico / estagiário** | É quem transcreve à mão hoje | Exportar para Word já formatado, sem retrabalho | "Vou ter de corrigir tudo à mesma" |
| **Sócio / gestor do escritório** (decide a compra) | Horas não faturáveis e risco de violar o sigilo profissional | Garantias de confidencialidade e custo previsível | "Para onde vão os ficheiros dos meus clientes?" |

O site fala para o **advogado** (quem sente a dor) e responde às perguntas do **sócio** (quem paga e responde pelo sigilo).

## 3. Proposta de valor

**Curta:** De horas a minutos, com o sigilo profissional garantido.

**Desenvolvida:** O Auditus converte gravações longas de audiências e inquirições em texto pesquisável, com cada intervenção atribuída a quem a disse e ligada ao segundo exato do áudio. É afinado para português de Portugal e para vocabulário jurídico, e todo o processamento é feito em servidores dedicados na União Europeia, sem enviar ficheiros para serviços públicos de IA. Quando o trabalho termina, os dados podem ser eliminados de forma definitiva.

## 4. Três pilares de mensagem

### Pilar 1 — Encontre em minutos o que levaria horas a ouvir
- **Promessa:** pesquisa por palavra-chave numa gravação de várias horas e salto direto ao minuto certo.
- **Prova:** timestamps por frase, clique na frase para ouvir o áudio original (história da Dra. Maria).
- **Não dizer:** "nunca mais precisa de ouvir a gravação". A verificação no áudio é parte do produto.

### Pilar 2 — Saiba sempre quem disse o quê
- **Promessa:** o texto vem separado por interveniente; os rótulos automáticos ("Locutor 1") passam a nomes reais ("Meritíssimo Juiz", "Testemunha João").
- **Prova:** exportação para Word/PDF com formato de ata, pronta a juntar ao processo.
- **Não dizer:** que a identificação é infalível em vozes sobrepostas. É o ponto onde o produto ainda está a melhorar.

### Pilar 3 — O sigilo profissional fica intacto
- **Promessa:** o áudio é processado em infraestrutura dedicada na UE, nunca é enviado para APIs públicas de IA (OpenAI, Google e semelhantes) e não é usado para treinar modelos.
- **Prova:** encriptação, eliminação definitiva a pedido ou automática (retenção zero), página de Segurança e RGPD com o percurso dos dados.
- **Não dizer:** "100 % seguro", "inviolável" ou certificações que não temos.

## 5. Tom de voz

**Sóbrio, rigoroso, confiável.** Escrevemos como um colega experiente, não como uma startup.

| Fazemos | Evitamos |
|---|---|
| Frases curtas e concretas, com números quando os temos | Superlativos ("revolucionário", "o melhor", "incrível") |
| Vocabulário do setor usado com rigor | Jargão técnico de IA ("LLM", "embeddings", "WER") fora da página de Segurança e da FAQ |
| Tratamento formal e impessoal ("o seu escritório", "pode exportar") | "Tu", "você", pontos de exclamação, emojis |
| Admitir limites (a IA erra; por isso há verificação no áudio) | Prometer perfeição |

### Sempre PT-PT

| Escrever | Nunca |
|---|---|
| ecrã | tela |
| telemóvel | celular |
| utilizador | usuário |
| ficheiro | arquivo |
| equipa | time |
| registo | cadastro |
| transferir / descarregar | baixar |
| palavra-passe | senha |
| escritório de advogados, sociedade de advogados | escritório de advocacia |

Na dúvida, confirmar no [Priberam](https://dicionario.priberam.org/) com a variante europeia.

## 6. Alternativas e onde falham

| Alternativa | O que oferece | Onde falha para o nosso público |
|---|---|---|
| **Transcrição manual** (advogado, estagiário, empresa de transcrição) | Fiável quando bem feita | Horas por gravação; caro; lento; o ficheiro circula por mais pessoas |
| **Ferramentas gerais de IA gratuitas** (assistentes de IA de grandes tecnológicas) | Grátis e rápidas; já há tutoriais a ensinar advogados a usá-las para audiências | O áudio de clientes vai para servidores de terceiros, muitas vezes fora da UE: risco direto para o sigilo profissional; sem identificação fiável de intervenientes nem formato de ata |
| **Plataformas de transcrição dos EUA** (ex.: Otter, Rev, Sonix) | Produtos maduros, muitas línguas | Segundo comparações públicas, várias não garantem armazenamento na UE; português genérico, sem foco jurídico PT-PT |
| **Plataformas europeias de transcrição** (ex.: Amberscript, HappyScribe, Trint) | Dizem guardar dados na UE e cumprir o RGPD; algumas têm certificação ISO 27001 | Generalistas: não são afinadas para jargão jurídico PT-PT nem para sotaques do continente e ilhas; sem exportação no formato de ata judicial portuguesa |
| **Iniciativas dos próprios tribunais** | O Estado anunciou ferramentas digitais com transcrição automática nos tribunais | Ainda por avaliar: âmbito, prazos e se chegam aos advogados. **Acompanhar** — pode reduzir a dor ou ser parceiro |

**Conclusão para o site:** "dados na UE" e "RGPD" são **condição mínima**, não diferenciação: as plataformas europeias já o dizem.
O Auditus diferencia-se por ser **feito para o setor jurídico português**: PT-PT e vocabulário jurídico, formato de ata, intervenientes nomeados, sem IA de terceiros e com retenção zero.
A mensagem de sigilo deve ser concreta (sem APIs públicas, sem treino com dados de clientes, eliminação definitiva), não apenas "cumprimos o RGPD".

> As afirmações sobre concorrentes vêm de páginas públicas e comparações de terceiros, não de testes nossos. **Não se nomeiam concorrentes no site** sem confirmação e revisão jurídica.

## 7. Identidade básica

### Nome
**Auditus** — em latim, "audição", "o ato de ouvir". Liga-se a *audiência* e a *ouvir com atenção*. Mantém-se.

### Slogan (escolher um)
1. **"De horas de audiência a minutos de leitura."** — recomendado: diz o benefício e o contexto.
2. "Cada palavra da audiência, ao seu alcance."
3. "Transcrição jurídica com sigilo profissional."

### Domínio (escolher um; disponibilidade **não verificada**)
1. `auditus.pt` — recomendado: curto e português. Registo na [DNS.pt](https://www.dns.pt).
2. `auditus.com.pt`
3. `auditus.legal` ou `auditus.eu` como alternativa se o `.pt` estiver ocupado.

Registar também as variantes principais e redirecioná-las para o domínio escolhido (#32).

## 8. Mensagens-chave por página

| Página | Objetivo | Mensagem principal | Mensagens de apoio | CTA |
|---|---|---|---|---|
| **Início** | Fazer o visitante perceber o valor em 5 segundos e pedir demo | De horas de audiência a minutos de leitura, com sigilo profissional garantido | Os 3 pilares; história da Dra. Maria; selos de confiança (UE, retenção zero, sem IA de terceiros) | Pedir demonstração |
| **Produto** | Mostrar como funciona | Pesquise, ouça e exporte: tudo ligado ao segundo exato da gravação | Upload de ficheiros grandes; intervenientes nomeados; verificação no áudio; Word/PDF em formato de ata; demo interativa com dados fictícios | Pedir demonstração |
| **Segurança e RGPD** | Remover a objeção do sócio | Os ficheiros dos seus clientes nunca saem da Europa nem passam por IA de terceiros | Percurso dos dados; encriptação; retenção zero; sem treino de modelos; subcontratantes | Ler a Política de Privacidade · Pedir demonstração |
| **Casos de uso** | Cada perfil reconhecer-se | Feito para quem trabalha com gravações de audiências | Um bloco por perfil da secção 2, com a dor e o resultado | Pedir demonstração |
| **Preços** | Dar referência sem afastar | Pague pelas horas de áudio que usa | Planos (valores a definir com o discovery); calculadora de horas poupadas | Pedir demonstração |
| **Contacto / Pedir demo** | Converter | Veja o Auditus a funcionar com uma gravação de exemplo | Prazo de resposta (a definir no #51); os dados do formulário ficam na UE | Enviar pedido |
| **FAQ** | Responder a objeções | Respostas diretas sobre precisão, tempos, formatos e privacidade | Objetivos da PRD apresentados como objetivos | Pedir demonstração |
| **Blog / Recursos** | Atrair pesquisa orgânica | Conteúdo útil sobre gravações, atas e RGPD em escritórios | Artigos práticos, não publicidade | Subscrever newsletter |
| **Sobre** | Dar rosto e credibilidade | Uma equipa portuguesa a resolver um problema do setor jurídico português | Quem somos; porquê este problema | Contactar |

## 9. O que podemos e não podemos afirmar

| Pode dizer-se | Não se diz (até haver prova) |
|---|---|
| "Objetivo: taxa de erro abaixo de 9 % em vocabulário jurídico português" | "99 % de precisão", "precisão total" |
| "Objetivo: processar em menos de um terço da duração do áudio" | "Transcrição instantânea", "em segundos" |
| "Processado em servidores dedicados na UE" | "Certificado ISO 27001" ou outras certificações |
| "Nunca enviamos os ficheiros para APIs públicas de IA" | "Aprovado pela Ordem dos Advogados" ou "admissível em tribunal" |
| "Pode eliminar os dados definitivamente a qualquer momento" | "Totalmente seguro", "inviolável" |
| Testemunhos e logótipos de clientes **com autorização escrita** | Testemunhos inventados ou de exemplo apresentados como reais |

## 10. Decisões em aberto

- [ ] Escolher o slogan (secção 7)
- [ ] Escolher e registar o domínio (secção 7, depois #32)
- [ ] Preços públicos ou "sob consulta" (depende do discovery; #45)
- [ ] Aprovação deste documento pelos três membros (critério de aceitação do #28)
