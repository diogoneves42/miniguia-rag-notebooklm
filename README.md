# Miniguia de Estudos com NotebookLM: Fundamentos de RAG

Este repositório documenta a construção de um caderno temático sobre **RAG (Retrieval-Augmented Generation)**, técnica usada para conectar LLMs a fontes externas e gerar respostas mais atualizadas, verificáveis e contextualizadas.

O objetivo foi organizar um material de estudo que sirva tanto para revisão rápida quanto para consulta prática em projetos reais de IA generativa.

## Contexto e objetivos

### Tema escolhido
**Fundamentos de RAG para aplicações com IA generativa**

### Objetivos de estudo
- Entender o que é RAG e por que essa abordagem reduz limitações de LLMs puros.
- Identificar os componentes centrais de um pipeline de RAG.
- Diferenciar conceitos como embeddings, chunking, recuperação, grounding e citações.
- Mapear boas práticas e limitações ao aplicar RAG em produtos reais.
- Criar prompts reutilizáveis para revisão e aprofundamento do tema.

## Curadoria de fontes

As fontes abaixo foram selecionadas para upload ou referência no NotebookLM. A escolha priorizou material aberto, técnico e complementar entre base conceitual, visão de mercado e implementação.

1. **Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks**  
   Link: https://arxiv.org/pdf/2005.11401  
   Tipo: PDF acadêmico  
   Motivo: artigo fundador do conceito de RAG.

2. **Retrieval-Augmented Generation for Large Language Models: A Survey**  
   Link: https://arxiv.org/pdf/2312.10997  
   Tipo: PDF acadêmico  
   Motivo: organiza a evolução do RAG em abordagens ingênuas, avançadas e modulares.

3. **Retrieval-augmented generation (RAG) in Azure AI Search**  
   Link: https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview  
   Tipo: artigo técnico  
   Motivo: explica arquitetura, desafios práticos e grounding.

4. **What is Retrieval-Augmented Generation (RAG)?**  
   Link: https://aws.amazon.com/what-is/retrieval-augmented-generation/  
   Tipo: artigo técnico  
   Motivo: fornece uma explicação objetiva com foco em aplicações corporativas.

5. **Optimizing your website for generative AI features on Google Search**  
   Link: https://developers.google.com/search/docs/fundamentals/ai-optimization-guide  
   Tipo: documentação oficial  
   Motivo: traz uma definição útil de RAG como mecanismo de melhoria de qualidade, atualização e confiabilidade.

## Engenharia de prompts e cicatrizes

Nesta etapa, o foco foi construir perguntas que forçassem o caderno a ir além de definição superficial. Abaixo estão os prompts principais, o que eu queria extrair e os ajustes necessários para melhorar a resposta.

| Prompt | Intenção | Resposta consolidada esperada | Ajuste / cicatriz |
| --- | --- | --- | --- |
| `Explique RAG como se eu fosse um desenvolvedor iniciante, em até 10 linhas.` | Obter uma visão simples e direta. | RAG combina busca + geração. Em vez de responder só com memória paramétrica do modelo, ele recupera trechos de fontes externas e usa esse contexto para responder com mais precisão. | Respostas muito genéricas tendem a ignorar embeddings, chunking e ranking. |
| `Quais são os componentes mínimos de um pipeline de RAG?` | Extrair a arquitetura básica. | Base documental, pré-processamento, chunking, embeddings, índice vetorial ou busca híbrida, recuperação, prompt com contexto e geração final. | Sem pedir “componentes mínimos”, o modelo costuma listar ferramentas em vez de blocos conceituais. |
| `Compare LLM puro vs. RAG em uma tabela com vantagens, limites e casos de uso.` | Produzir contraste prático. | LLM puro é mais simples e rápido para conhecimento geral; RAG é melhor para conteúdo específico, atualizado e citável. | Se a instrução não exigir tabela, a resposta perde legibilidade. |
| `Quais erros mais comuns degradam a qualidade de um sistema RAG?` | Encontrar troubleshooting real. | Chunking ruim, recuperação irrelevante, contexto excessivo, documentos desatualizados, ausência de avaliação e falta de citações. | Sem pedir “erros mais comuns”, o modelo tende a repetir boas práticas sem expor falhas. |
| `Crie um glossário de RAG com definições curtas e sem jargão desnecessário.` | Consolidar revisão. | Termos como embedding, chunk, top-k, reranking, grounding, hallucination, recall e precisão. | Se não limitar o jargão, a resposta fica excessivamente acadêmica. |
| `Monte um plano de estudo de 30 minutos para revisar este tema antes de uma entrevista.` | Transformar conteúdo em uso prático. | Revisão rápida de definição, pipeline, riscos, métricas e exemplos de aplicação. | Sem restringir o tempo, a resposta vira uma trilha extensa demais. |

### Principais dificuldades encontradas

- **Respostas amplas demais**: quando o prompt pedia “explique RAG”, a resposta vinha correta, mas superficial.
- **Mistura entre conceito e ferramenta**: alguns resultados confundiam arquitetura de RAG com nomes de frameworks.
- **Excesso de abstração**: sem pedir exemplos, o conteúdo ficava teórico demais para revisão prática.
- **Pouca rastreabilidade**: quando o prompt não exigia base nas fontes, a IA podia responder de forma plausível, mas sem lastro claro.

### Estratégias que melhoraram os resultados

- Pedir formato explícito: tabela, checklist, glossário ou resumo em tópicos.
- Delimitar nível de profundidade: iniciante, técnico ou entrevista.
- Exigir comparação: `compare`, `diferencie`, `mostre trade-offs`.
- Forçar ancoragem nas fontes: `responda com base apenas nas fontes enviadas`.
- Solicitar saída útil para revisão: `em até 10 linhas`, `em bullets`, `com exemplos`.

## Miniguia de estudo

### 1. O que é RAG

RAG é uma arquitetura que combina um modelo de linguagem com um mecanismo de recuperação de informação. Em vez de depender apenas do que o modelo aprendeu no treinamento, a resposta é gerada com apoio em documentos recuperados no momento da consulta. Isso aumenta atualização, precisão e capacidade de citar fontes.

### 2. Como um pipeline de RAG funciona

1. Coleta dos documentos.
2. Quebra do conteúdo em partes menores.
3. Conversão dos trechos em embeddings.
4. Armazenamento em índice vetorial ou sistema de busca híbrida.
5. Recuperação dos trechos mais relevantes para a pergunta.
6. Montagem do prompt com contexto recuperado.
7. Geração da resposta final com base nesse contexto.

### 3. Por que usar RAG

- Reduz dependência exclusiva da memória do modelo.
- Permite trabalhar com conteúdo privado ou atualizado.
- Melhora verificabilidade ao mostrar trechos e referências.
- É mais barato e prático do que retreinar um modelo para cada base nova.

### 4. Limitações de RAG

- Se a recuperação falhar, a resposta final também falha.
- Documentos mal segmentados reduzem a relevância dos trechos.
- Contexto demais pode poluir o prompt.
- Nem todo sistema com busca semântica tem boa groundedness.
- RAG não elimina alucinação; ele apenas reduz o risco.

### 5. Boas práticas

- Definir chunking com critério semântico, não só por tamanho fixo.
- Testar busca vetorial, lexical e híbrida.
- Avaliar recuperação e resposta separadamente.
- Manter fontes atualizadas e confiáveis.
- Exigir citações ou trechos de apoio sempre que possível.

## Glossário

| Termo | Definição |
| --- | --- |
| **RAG** | Técnica que usa recuperação de documentos para apoiar a geração de respostas. |
| **LLM** | Modelo de linguagem de grande porte capaz de gerar texto. |
| **Embedding** | Representação numérica de um texto usada para medir similaridade semântica. |
| **Chunking** | Divisão do documento em trechos menores para indexação e recuperação. |
| **Índice vetorial** | Estrutura usada para armazenar embeddings e buscar conteúdos semanticamente próximos. |
| **Top-k** | Quantidade de trechos recuperados para compor o contexto. |
| **Reranking** | Reordenação dos resultados para melhorar relevância. |
| **Grounding** | Ancoragem da resposta em fontes específicas. |
| **Hallucination** | Resposta inventada ou não sustentada pela base. |
| **Busca híbrida** | Combinação de busca semântica com busca por palavra-chave. |

## Prompts reutilizáveis

### Para entendimento inicial
`Explique [tema] em linguagem simples, com definição, exemplo e aplicação prática.`

### Para revisão técnica
`Resuma [tema] em tópicos, destacando arquitetura, vantagens, limitações e boas práticas.`

### Para comparação
`Compare [conceito A] e [conceito B] em uma tabela com diferenças, vantagens, riscos e casos de uso.`

### Para diagnóstico
`Liste os erros mais comuns ao implementar [tema] e proponha formas de corrigir cada um.`

### Para entrevista
`Simule 5 perguntas de entrevista sobre [tema] e responda como um candidato pleno.`

### Para revisão baseada em fonte
`Responda apenas com base nas fontes fornecidas. Se algo não estiver nas fontes, diga explicitamente.`

## Estrutura do repositório

```text
miniguia-rag-notebooklm/
├── README.md
└── docs/
    └── entrega-dio.md
```

## Como usar este material no NotebookLM

1. Criar um novo notebook com o tema `Fundamentos de RAG`.
2. Adicionar as 5 fontes listadas acima.
3. Executar os prompts da seção de engenharia de prompts.
4. Refinar as perguntas até obter respostas mais curtas, comparativas e citáveis.
5. Consolidar a revisão final com base no miniguia deste repositório.

## Entrega na DIO

O texto sugerido para a descrição da entrega está em [docs/entrega-dio.md](docs/entrega-dio.md).

Se quiser publicar este projeto como portfólio técnico, uma boa descrição curta é:

> Caderno temático sobre Retrieval-Augmented Generation (RAG), com curadoria de fontes abertas, registro de prompts, troubleshooting e miniguia final de revisão para IA generativa.
