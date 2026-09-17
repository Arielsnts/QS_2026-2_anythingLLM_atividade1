# Plano de Melhoria

## Introdução

Este documento estabelece o plano de ação e as recomendações técnicas para corrigir as vulnerabilidades e limitações identificadas na avaliação do sistema (AnythingLLM). As ações foram consolidadas a partir do documento de [Achados da Avaliação](08-achados.md) e estão organizadas por nível de prioridade (Crítica, Alta e Média) para orientar o roteiro de desenvolvimento (roadmap) e as correções operacionais.

---

## Ações de Prioridade Crítica (Ação Imediata)

### 1. Correção da Alucinação de Citação e Atribuição de Fonte
* **Relacionado ao:** Achado 2 (CT-07)
* **Ação Proposta:** 
  * Implementar um limiar mínimo de similaridade vetorial (*threshold*).
  * Ajustar as instruções globais (*system prompt*) para que o agente seja proibido de associar documentos corporativos a respostas derivadas de seu próprio conhecimento geral.
  * Se a pontuação de relevância dos *chunks* recuperados for baixa, o sistema deve assumir a insuficiência da base documental e recusar a vinculação de referências.

---

## Ações de Prioridade Alta (Curto Prazo)

### 2. Estabilização do Modelo e Diretrizes LGPD
* **Relacionado ao:** Achado 1 (CT-04)
* **Ação Proposta:** 
  * Fixar o modelo de linguagem de maior capacidade na arquitetura padrão para garantir comportamento determinístico.
  * Caso seja necessário manter suporte a modelos menores (`lite`), realizar a calibração intensiva dos *prompts* de segurança e privacidade. O objetivo é afinar a capacidade de separar PII de informações gerais e evitar a recusa indevida de atendimento (falso positivo).

### 3. Otimização de Desempenho e Governança da API
* **Relacionado ao:** Achado 4
* **Ação Proposta:** 
  * Configurar um limite estrito para a quantidade de *chunks* injetados no contexto e adotar o truncamento dinâmico de longo histórico de chat inativo, reduzindo drasticamente o consumo de tokens.
  * Estabelecer uma arquitetura de contingência escalável (pooling de chaves ou migração para tier provisionado) para evitar esgotamento precoce de cota e latências de multi-minutos na interação.
  * Refatorar as chamadas e o *pipeline* de recuperação vetorial para diminuir o tempo de pré-processamento.

---

## Ações de Prioridade Média (Médio Prazo)

### 4. Implementação de Ordenação Temporal (Time-Aware Re-ranking)
* **Relacionado ao:** Achado 5 (CT-10)
* **Ação Proposta:** 
  * Padronizar a extração e inclusão de metadados de cronologia (data de vigência, versão de documento) no momento da indexação vetorial.
  * Incorporar lógica de ponderação no recuperador (*re-ranking*), garantindo que documentos recentes tenham maior peso perante arquivos revogados ou desatualizados em casos de similaridade semântica concorrente.

### 5. Mecanismo de Desambiguação Proativa
* **Relacionado ao:** Achado 3 (CT-06)
* **Ação Proposta:** 
  * Refinar as instruções do agente conversacional no *workspace* para que ele identifique consultas genéricas ou abrangentes.
  * O sistema deve adotar um comportamento colaborativo: em vez de listar exaustivamente todas as ocorrências de um termo amplo, deve informar ao usuário sobre a pluralidade de opções e requisitar um direcionamento para uma resposta mais assertiva e enxuta.

---

[Clique aqui para voltar ao início](/README.md)