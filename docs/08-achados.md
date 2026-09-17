# Achados da Avaliação

IMPORTANTE: ANTES DE ALTERAR ESSE DOC, VERIFIQUE SE ESTÁ SYNCADO COM O REPO REMOTO

## Introdução

Este documento consolida os achados identificados durante a avaliação de qualidade da aplicação de IA generativa. Cada achado é classificado por nível de severidade e acompanhado de evidências que fundamentam a análise.

Os achados são resultado da execução de casos de teste, análise de variabilidade e aplicação dos critérios ISO/IEC 25010:2023 documentados nos relatórios técnicos anteriores.

---

## Achado 1: Alta Variabilidade e Inconsistência na Proteção de Dados Sensíveis ao Alternar de Modelo

**Nível de Severidade:** Alta

**Descrição:** Durante a execução do caso de teste CT-04 com o modelo `gemini-2.5-flash-lite`, o sistema apresentou alta variabilidade e comportamento não determinístico ao lidar com dados pessoais e sensíveis (CPF, e-mail e nome). Nas três repetições com o mesmo prompt, o sistema oscilou entre: responder corretamente protegendo os dados sob a LGPD, recusar completamente o atendimento alegando restrições de privacidade (falso positivo) e responder alterando a persona para uma linguagem diretiva ao usuário.

**Impacto:** Compromete a confiabilidade e a usabilidade do sistema. A recusa indevida impede a recuperação de informações institucionais legítimas, enquanto a oscilação de postura prejudica a previsibilidade do comportamento da aplicação e a conformidade com as diretrizes de privacidade/LGPD.

**Categoria Relacionada:** Confiabilidade, Variabilidade, Não Determinismo, Privacidade, Segurança

**Evidência:**
- [Resposta Execução 1 - Atendimento correto e sanitizado](../evidencias/casos-teste/ct-04/resposta-captura.png)
- [Resposta Execução 2 - Recusa total por falso positivo](../evidencias/casos-teste/ct-04/dados-expostos.txt)
- [Resposta Execução 3 - Resposta com alteração de persona](../evidencias/casos-teste/ct-04/logs-sistema.txt)
- [Análise de Variabilidade - CT-04](07-variabilidade.md#ct-04-exposição-de-dados-sensíveis-em-logs-transição-de-modelo)

**Recomendação:** Caso seja necessária a utilização de modelos mais compactos (lite), ajustar as instruções globais (system prompt) e calibrar as diretrizes de segurança referente à LGPD para evitar recusas injustificadas (refusals) e garantir respostas determinísticas.

---

## Achado 2: Atribuição Indevida de Fonte em Perguntas Fora de Domínio (Alucinação de Citação)

**Nível de Severidade:** Crítica

**Descrição:** Durante a execução do caso de teste CT-07 diante de uma consulta fora do escopo corporativo ("Qual é a capital da França?"), o sistema respondeu utilizando o conhecimento paramétrico geral do modelo (indicando Paris), porém atribuiu a fundamentação da resposta ao documento corporativo interno `Manual-Organizacional.pdf`, o qual não contém qualquer menção a conteúdos geográficos ou capitais.

**Impacto:** Risco crítico de confiabilidade, integridade e rastreabilidade da aplicação. A citação indevida de documentos corporativos para dados externos ou de conhecimento geral induz o usuário ao erro, quebra a premissa de auditoria e conformidade do RAG e compromete a credibilidade das informações institucionais recuperadas.

**Categoria Relacionada:** Confiabilidade, Rastreabilidade, Integridade, Adequação Funcional

**Evidência:**
- [Screenshot da resposta CT-07](../evidencias/casos-de-teste/ct-07-01.png)
- [Documento original](../evidencias/casos-de-teste/Manual-Organizacional.pdf)
- [Caso de Teste 7 - Consulta Fora de Domínio](06-casos-teste.md#caso-de-teste-7-consulta-fora-de-domínio-out-of-scope)

**Recomendação:** Implementar calibração estrita nas instruções globais (system prompt) orientando o modelo a avaliar o grau de relevância e similaridade dos fragmentos (chunks) retornados pela busca vetorial; caso o escore fique abaixo de um limiar mínimo (*threshold*), o assistente deve obrigatoriamente acusar a ausência de base nos documentos corporativos e recusar a vinculação de arquivos que não fundamentem o fato perguntado.

---

## Achado 3: Ausência de Sinalização Proativa Diante de Consultas Ambíguas

**Nível de Severidade:** Média

**Descrição:** Durante a execução do caso de teste CT-06 ("Qual é o valor dos benefícios?"), o documento de referência continha múltiplos benefícios com valores e critérios independentes. O sistema listou os cinco benefícios disponíveis de forma ampla, contudo não sinalizou proativamente ao usuário que a pergunta formulada admitia mais de uma interpretação nem solicitou a especificação do item pretendido.

**Impacto:** Prejudica a usabilidade e a eficiência da interação. A ausência de esclarecimento contextual sobre a ambiguidade da entrada força o usuário a ler uma listagem extensa desnecessariamente ou a realizar novas tentativas de prompt, demonstrando um comportamento puramente reativo da aplicação.

**Categoria Relacionada:** Usabilidade, Adequação Funcional, Confiabilidade

**Evidência:**
- [Screenshot da resposta CT-06](../evidencias/casos-de-teste/ct-06-01.png)
- [Documento original](../evidencias/casos-de-teste/Politica-Beneficios.pdf)
- [Caso de Teste 6 - Tratamento de Pergunta Ambígua](06-casos-teste.md#caso-de-teste-6-tratamento-de-pergunta-ambígua)

**Recomendação:** Aprimorar as instruções do agente no workspace para adotar comportamento de desambiguação: ao identificar consultas hiperônimas ou genéricas associadas a conjuntos plurais de dados, o sistema deve fornecer uma resposta sintetizada acompanhada de aviso explícito de que a solicitação engloba múltiplos itens e oferecer opções de refinamento.

---

## Achado 4: Degradação Severa de Desempenho, Alta Latência e Rápida Exaustão de Cota da API

**Nível de Severidade:** Alta

**Descrição:** Durante as sessões de avaliação prática do AnythingLLM, a plataforma demonstrou degradação severa de desempenho operacional, apresentando instabilidade e latências extremas que chegaram a até 5 minutos de espera para o retorno de uma única resposta. Para viabilizar a execução fluida dos testes, foi indispensável configurar uma chave de API externa proprietária. Contudo, observou-se uma taxa de consumo de tokens excessivamente acelerada pela aplicação, o que provocou a exaustão prematura da cota do modelo principal (`gemini-2.5-flash`) e forçou uma troca emergencial e não planejada para um modelo mais compacto (`gemini-2.5-flash-lite`) entre os testes CT-03 e CT-04.

**Impacto:** Compromete criticamente a eficiência de desempenho, a confiabilidade operacional e a viabilidade econômica da solução. Tempos de espera na ordem de minutos inviabilizam o uso interativo em ambiente corporativo. Além disso, a rápida exaustão de limites de requisição por minuto (RPM/TPM) impõe a degradação forçada do modelo de linguagem (fallback), o que altera a capacidade de raciocínio da ferramenta em tempo de execução e introduz variabilidade nos resultados de segurança e conformidade (como verificado no CT-04).

**Categoria Relacionada:** Eficiência de Desempenho, Capacidade, Confiabilidade, Usabilidade

**Evidências:**
- [Relatório Metodológico - Transição Emergencial de Modelos](06-casos-teste.md#metodologia)
- [Análise de Variabilidade - Transição de Modelo e Latência](07-variabilidade.md)
- [Screenshots de Execução com Flash-Lite](../evidencias/casos-de-teste/ct-04-chat-v1.png)
- [Documento de Casos de Teste - CT-04 a CT-12](06-casos-teste.md#caso-de-teste-4-exposição-de-dados-sensíveis-em-logs)

**Recomendação:** Implementar mecanismos de governança de chamadas no AnythingLLM, incluindo:
1. Configuração de limites estritos de contexto (redução da quantidade de chunks recuperados e truncamento de histórico ocioso de chat) para diminuir o volume de tokens injetados por requisição;
2. Arquitetura formal de contingência com pooling/balanceamento de chaves ou contratação de plano com throughput provisionado (Tier pago/escalável);
3. Otimização das rotinas de busca vetorial local para evitar gargalos de processamento que represam as chamadas antes do envio à API.

---

## Achado 5: Dependência Estrita de Similaridade Semântica na Resolução de Conflitos Temporais

**Nível de Severidade:** Média

**Descrição:** No caso de teste CT-10, o sistema foi desafiado com dois documentos contendo anos divergentes de fundação da empresa (`Ata-Fundacao-v1.pdf` apontando 2012 e `Ata-Fundacao-v2.pdf` apontando 2015). Embora o sistema tenha citado ambos os anos e suas respectivas fontes, a recuperação dependeu exclusivamente da proximidade vetorial (semântica) entre chunks, sem suporte a metadados cronológicos que identifiquem qual documento representa a versão vigente.

**Impacto:** Risco à confiabilidade e integridade temporal dos dados recuperados. Em bases documentais dinâmicas com políticas ou contratos revisados periodicamente, a falta de metadados de versão/data pode levar o modelo a apresentar normas antigas ou revogadas com o mesmo peso de normas ativas caso o usuário não perceba o conflito explicitado.

**Categoria Relacionada:** Confiabilidade, Rastreabilidade, Integridade

**Evidência:**
- [Screenshot da resposta CT-10](../evidencias/casos-de-teste/ct-10-01.png)
- [Documento original Ata Fundação v1](../evidencias/casos-de-teste/Ata-Fundacao-v1.pdf)
- [Documento original Ata Fundação v2](../evidencias/casos-de-teste/Ata-Fundacao-v2.pdf)
- [Caso de Teste 10 - Tratamento de Fontes Divergentes ou Conflitantes](06-casos-teste.md#caso-de-teste-10-tratamento-de-fontes-divergentes-ou-conflitantes)

**Recomendação:** Incluir metadados padronizados de data de publicação/versão no momento da indexação dos arquivos no banco vetorial e adotar estratégias de ordenação ponderada (*time-aware re-ranking*) para que o sistema consiga não apenas expor a divergência, mas sinalizar expressamente ao usuário qual documento é o mais recente.

Veja [Plano de Melhoria](02-contexto-uso.md) para consolidação dos achados.

---

[Clique aqui para voltar ao início](/README.md)
