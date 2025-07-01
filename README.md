# Estudo sobre decisões racionais no xadrez com modelos de linguagem

---

## 1. Resumo

Estudo sobre como LLMs podem tomar decisões estratégicas de forma racional, buscando ganhos em curto, médio e longo prazo no jogo de xadrez. O projeto investiga o comportamento de modelos de linguagem em cenários de decisão autônoma, sem apoio de motores em tempo real. Utiliza vetorização de posições FEN para buscas contextuais, Chain of Verification para garantir jogadas legais e aprendizado contínuo por meio de autojogos e análises 

---

## 2. Objetivo

Criar um site de xadrez onde uma IA baseada em LLM jogue partidas autonomamente, decidindo sozinha as jogadas (sem ajuda de motores como Stockfish durante o jogo) e que aprimore sua habilidade com o tempo por meio de aprendizado e análise.

---

## 3. Objetivos de Metodologia

1. **Base de Conhecimento**  
   Construir uma base com muitas posições representadas em FEN.  
   Cada posição terá as 3 melhores jogadas segundo Stockfish, acompanhadas de explicações estratégicas.

2. **Vetorização**  
   Converter as posições FEN em embeddings vetoriais para criar um índice que permita buscar rapidamente as posições mais similares a uma dada posição durante a partida.

3. **Busca em Partida**  
   Durante o jogo, para a posição atual, buscar as 3 posições mais parecidas no banco.

4. **Construção do Prompt para a LLM**  
   Criar um prompt que envie para a LLM a posição atual, junto com as 3 posições similares, suas melhores jogadas e as explicações estratégicas correspondentes.

5. **Resposta da LLM**  
   A LLM deve responder com dois segmentos:  
   - `<JSON>` contendo a jogada escolhida no formato:  
     ```json
     {
       "response": {
         "start": "casa_inicial",
         "target": "casa_alvo",
         "type": "tipo_da_peça"
       }
     }
     ```  
   - `<THOUGHT>` explicando a razão da escolha da jogada, fundamentando a decisão de forma clara e estratégica.

6. **Chain of Verification (CoV)**  
   Implementar um processo para:  
   - Verificar se a jogada é legal segundo as regras do xadrez.  
   - Se inválida, solicitar à LLM que revise e corrija a jogada e a explicação.  
   - Repetir a verificação até a jogada ser considerada válida e coerente.

7. **Execução da Jogada**  
   Após aprovação pela Chain of Verification, executar a jogada no tabuleiro.

8. **Avaliação Offline**  
   Avaliar a qualidade da jogada feita pela LLM usando Stockfish para fornecer feedback.

9. **Atualização da Base**  
   Jogadas bem avaliadas são inseridas na base de conhecimento para fortalecer o banco vetorial, melhorando o contexto das próximas decisões.

10. **Autojogos e Jogos contra Humanos**  
    Implementar partidas de self-play e contra humanos para coletar dados adicionais que alimentem o aprendizado da LLM.

---

## 4. Tecnologias úteis

- Utilização da notação **FEN** (Forsyth–Edwards Notation) para representar o estado do tabuleiro em texto.  
- FEN facilita o armazenamento, indexação e recuperação de posições semelhantes.  
- Cada FEN contém informações completas da posição, do jogador a jogar, direitos de roque, possibilidade de captura en passant, contagem de meio-lances e número da jogada.

---

## 5. Temas e Papers Interessantes para Referência

### Self-play adversarial em LLMs
- "Self-playing Adversarial Language Game Enhances LLM Reasoning"  
  [arXiv link](https://arxiv.org/pdf/2404.10642)  

### Chain of Thought (CoT)
- "Chain of Thought Prompting Elicits Reasoning in Large Language Models"  
  [arXiv link](https://arxiv.org/pdf/2201.11903)

### Retrieval-Augmented Generation (RAG)
- "Retrieval-Augmented Generation for Large Language Models: A Survey"  
  [arXiv link](https://arxiv.org/pdf/2312.10997)

### Chain of Verification (CoV)
- "CHAIN-OF-VERIFICATION REDUCES HALLUCINATION IN LARGE LANGUAGE MODELS"  
  [arXiv link](https://arxiv.org/pdf/2309.11495)


---

