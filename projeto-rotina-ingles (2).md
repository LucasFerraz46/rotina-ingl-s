# Projeto: Rotina — Site de aulas diárias de inglês

> Documento de referência do projeto. Cole este conteúdo em uma nova conversa com o Claude para retomar o trabalho de onde parou.

## 1. Objetivo

Criar um site pessoal (HTML/CSS/JS puro, sem framework) para aprender inglês de verdade, com **aulas diárias de 50 minutos**, cobrindo:
- Gramática
- Leitura
- Compreensão auditiva
- Expressão oral

## 2. Perfil do aluno

- **Nível atual:** Iniciante (A1) — quase do zero
- **Idioma alvo:** Inglês
- **Idioma das instruções:** Português
- **Áudio/escuta:** combinação de síntese de voz do navegador (Text-to-Speech) + áudios/vídeos externos linkados
- **Fala:** quer gravar a própria voz e comparar com a pronúncia alvo (reconhecimento de voz do navegador)

## 3. Decisões técnicas

- **Stack:** HTML + CSS + JavaScript puro (sem React, sem Next.js, sem build)
- **Persistência:** localStorage do navegador (progresso, streak, dias concluídos) — nada de backend/servidor por enquanto
- **Text-to-Speech:** API nativa `SpeechSynthesis` do navegador
- **Reconhecimento de voz:** API nativa `SpeechRecognition` do navegador
- **Conteúdo das aulas:** 100% original, escrito por nós — nada copiado de sites de terceiros (BBC Learning English e British Council foram descartados como fonte direta por causa de direitos autorais; podem no máximo ser linkados como referência externa)
- **Inspiração conceitual (não código):** repositório [Orion](https://github.com/angelopedroso/Orion) (licença Apache 2.0) — conceito de "mineração de frases" (coletar palavras novas → gerar frases → estudar)
- **Integração GitHub/VS Code:** decidimos trabalhar manualmente por aqui primeiro (via chat), em vez de configurar Claude Code + VS Code + GitHub. Isso pode ser revisitado depois se o projeto crescer.

## 4. Estrutura de uma aula (50 minutos)

| Bloco | Duração | Conteúdo |
|---|---|---|
| 1. Aquecimento + Gramática | 15 min | Revisão do dia anterior + explicação + exemplos + exercícios |
| 2. Compreensão auditiva | 10 min | Áudio (TTS ou externo) + perguntas de compreensão |
| 3. Leitura | 10 min | Texto curto no nível do dia, vocabulário novo destacado |
| 4. Expressão oral | 10 min | Gravação da voz + comparação de pronúncia |

Trilha planejada: 14 dias visíveis na barra lateral (expansível), começando pelo **Dia 1 — Greetings & Introductions** (verbo *to be*, cumprimentos, apresentações).

## 5. Identidade visual (design tokens)

- **Fundo:** `#F7ECE7` (blush suave)
- **Superfície/cards:** `#FFF9F6`
- **Texto principal:** `#331F1A`
- **Texto secundário:** `#8A6A61`
- **Linhas/bordas:** `#EAD3CA`
- **Cor principal (vermelho terracota):** `#B23A2E`
- **Cor secundária (dourado):** `#C98F3F`
- **Cor de destaque profundo (vinho):** `#7A2620`
- **Tipografia:** Fraunces (display/serifada) + Work Sans (corpo) + IBM Plex Mono (números, tempo, dados)
- **Elemento de assinatura:** "dial" circular de 50 minutos, dividido em 3 arcos coloridos proporcionais ao tempo de cada bloco da aula

## 6. Status atual (o que já existe)

Arquivo: `index.html`

- [x] Estrutura geral do site (sidebar + área principal)
- [x] Barra lateral com trilha de 14 dias e contador de streak
- [x] Dial de progresso de 50 minutos (SVG, elemento de assinatura visual)
- [x] Paleta de cores em tons de vermelho (terracota, dourado, vinho)
- [x] **Dicionário instantâneo**: caixa de busca sempre visível no topo da aula. Primeiro consulta um dicionário local (palavras da aula, resposta instantânea), e se não encontrar, busca automaticamente na API gratuita **MyMemory Translation** (`api.mymemory.translated.net`), sem precisar de chave/cadastro
- [x] **Bloco 1 (Gramática) — Dia 1 completo**: explicação do verbo *to be* (afirmativa e negativa), tabela de conjugação, 6 exemplos com tradução, 2 exercícios interativos (preencher lacunas + múltipla escolha) com correção automática
- [x] **Bloco 2 (Escuta) — Dia 1 completo**: diálogo de apresentação com áudio via Text-to-Speech (voz sintetizada do navegador), reproduzível linha a linha ou completo, + 4 perguntas de compreensão com correção
- [x] **Bloco 3 (Leitura) — Dia 1 completo**: texto curto original com vocabulário novo destacado
- [x] **Bloco 4 (Fala) — Dia 1 completo**: reprodução da frase-alvo (TTS) + gravação da voz do usuário via reconhecimento de voz do navegador, com cálculo de % de aproximação com a frase alvo
- [ ] Sistema de progresso/streak funcionando de fato (hoje é só visual, não salva ainda em localStorage)
- [ ] Conteúdo dos Dias 2 em diante (só o Dia 1 tem conteúdo completo)
- [ ] Publicação no GitHub Pages (guia já formulado, aguardando o usuário executar)

## 7. Como retomar

1. Cole este documento inteiro no início de uma nova conversa com o Claude.
2. Anexe (ou peça para eu recriar) o arquivo `index.html` atual.
3. Diga qual é o próximo passo que quer atacar (ex: "vamos criar o conteúdo do Dia 2" ou "vamos fazer o progresso salvar de verdade").

## 8. Histórico de decisões (changelog)

- **v0.1** — Definido escopo do projeto: aulas diárias completas (não só flashcards), nível A1, HTML puro.
- **v0.1** — Descartada integração com BBC/British Council como fonte de conteúdo (direitos autorais).
- **v0.1** — Avaliado repositório Orion no GitHub; aproveitado só o conceito, não o código (stack diferente: Next.js vs HTML puro).
- **v0.1** — Criado esqueleto inicial do site (`index.html`) com estrutura, navegação e layout do Dia 1.
- **v0.2** — Paleta de cores atualizada para tons de vermelho (terracota, dourado, vinho).
- **v0.3** — Pesquisado syllabus CEFR A1 (fonte: guias públicos de referência) e definida trilha de 20 dias, do mais básico ao mais complexo.
- **v0.3** — Conteúdo completo do Dia 1 implementado nos 4 blocos (gramática, escuta, leitura, fala), com exercícios interativos e funcionalidade real de áudio (TTS) e gravação de voz (SpeechRecognition).
- **v0.4** — Exercícios e exemplos do Dia 1 expandidos (mais frases, mais questões nos quizzes).
- **v0.4** — Dicionário instantâneo criado: local primeiro, com fallback para API gratuita de tradução (MyMemory) quando a palavra não está no dicionário da aula.
- **v0.5** — Definido plano de publicação via GitHub Pages (gratuito, HTTPS automático — necessário para microfone e tradução online funcionarem em produção).

<!-- Ao continuar o projeto, adicione novas entradas aqui com a data e o que mudou. -->
