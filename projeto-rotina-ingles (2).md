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

Trilha atual: **30 dias**, do A1 básico até uma ponte com A2 (ver seção 6 para a lista completa de tópicos). Estrutura orientada a dados: cada dia é um "registro" no objeto `lessons` do JavaScript (gramática, diálogo, leitura, fala), renderizado dinamicamente — não é mais HTML repetido por dia.

## 5. Identidade visual (design tokens)

- **Fundo:** `#F7ECE7` (blush suave)
- **Superfície/cards:** `#FFF9F6`
- **Texto principal:** `#331F1A`
- **Texto secundário:** `#8A6A61`
- **Linhas/bordas:** `#EAD3CA`
- **Cor principal (vermelho terracota):** `#B23A2E`
- **Cor secundária (dourado):** `#C98F3F`
- **Cor de destaque profundo (vinho):** `#7A2620`
- **Verde de sucesso (streak/correção):** `#4A7A45`
- **Tipografia:** Fraunces (display/serifada) + Work Sans (corpo) + IBM Plex Mono (números, tempo, dados)
- **Elemento de assinatura:** "dial" circular de 50 minutos, dividido em 3 arcos coloridos proporcionais ao tempo de cada bloco da aula

## 6. Status atual (o que já existe)

Arquivo: `index.html` (arquitetura orientada a dados — objeto `lessons` no JS)

- [x] Estrutura geral do site (sidebar + área principal), agora com navegação real entre dias (clique no menu lateral, ou botões "Dia anterior / Próximo dia")
- [x] **30 dias de conteúdo completo**, cada um com os 4 blocos (gramática, escuta, leitura, fala), história contínua com dois personagens recorrentes (Marcos, brasileiro aprendendo inglês, e Anna, amiga canadense) para dar coesão e contexto real ao vocabulário
- [x] Trilha de tópicos: to be → preposições → artigos → plural → possessivos → there is/are → demonstrativos → present simple (afirm./neg./perguntas) → números e horas → advérbios de frequência → can/can't → adjetivos → família → quantificadores → pronomes objeto → present continuous → comparativos → superlativos → imperativos/direções → comida (would like) → clima → datas → past simple (to be, regulares, irregulares) → going to (futuro) → preposições de tempo → must/should → revisão geral (dia 30)
- [x] Cada dia tem: explicação de gramática + 4 exemplos traduzidos, 2 exercícios interativos (preencher lacunas + múltipla escolha) com correção automática, diálogo com áudio via TTS (linha a linha ou completo) + 2-3 perguntas de compreensão, texto de leitura com vocabulário destacado, frase-alvo para gravação de voz com % de aproximação
- [x] **Streak funcional de verdade**: salvo em `localStorage`. Botão "Marcar dia como concluído" em cada aula. Lógica: se o último dia concluído foi ontem, o streak soma +1; se foi hoje, não muda; se foi antes de ontem (quebrou a sequência), reinicia para 1. Progresso (X/30 dias) e streak exibidos na barra lateral, com bolinhas verde/dourado marcando dias concluídos
- [x] Progresso persiste entre visitas (mesmo navegador) — fecha o site e volta no dia seguinte que o streak e os dias concluídos continuam salvos
- [x] Paleta de cores em tons de vermelho (terracota, dourado, vinho)
- [x] **Dicionário instantâneo**: caixa de busca sempre visível no topo. Primeiro consulta um dicionário local (~60 palavras das aulas, resposta instantânea), e se não encontrar, busca automaticamente na API gratuita **MyMemory Translation** (`api.mymemory.translated.net`), sem precisar de chave/cadastro
- [x] Publicado no GitHub Pages: `https://lucasferraz46.github.io/rotina-ingl-s/`
- [ ] Nível A2 completo (hoje o dia 30 é uma "ponte" de revisão — o conteúdo A2 pleno ainda não foi criado)
- [ ] Dicionário local ainda cobre só o vocabulário das 30 aulas — o resto já é coberto pela API online, mas não há cache dessas buscas
- [ ] Sem sistema de "dia bloqueado até completar o anterior" — hoje a navegação é livre entre todos os 30 dias

## 7. Como retomar

1. Cole este documento inteiro no início de uma nova conversa com o Claude.
2. Anexe (ou peça para eu recriar) o arquivo `index.html` atual.
3. Diga qual é o próximo passo (ex: "vamos criar o nível A2" ou "vamos travar a navegação até completar o dia anterior").

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
- **v0.6** — Site publicado com sucesso em `https://lucasferraz46.github.io/rotina-ingl-s/` (corrigido erro de nome de arquivo duplicado, `index (3).html` → `index.html`).
- **v0.7** — Reestruturação completa: site migrado de HTML estático (só Dia 1) para arquitetura orientada a dados. Criados **30 dias de conteúdo completo e diversificado**, com história contínua (Marcos e Anna) amarrando o vocabulário. Sistema de **streak real implementado**, salvando progresso em localStorage com lógica de sequência consecutiva.

<!-- Ao continuar o projeto, adicione novas entradas aqui com a data e o que mudou. -->
