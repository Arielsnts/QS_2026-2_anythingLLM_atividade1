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

## Achado n: Exemplo de achado

**Nível de Severidade:** Muito Alta

**Descrição:** Execuções idênticas do mesmo prompt produzem respostas semanticamente diferentes. Em um caso, a aplicação retornou código correto; em outro, código com erro lógico. Não há indicação de quando a resposta é derivada de alucinação.

**Impacto:** Impede confiança em respostas técnicas. Usuários não conseguem determinar se a resposta é confiável ou se foi gerada sem fundamentação real.

**Categoria Relacionada:** Confiabilidade, Variabilidade, Não Determinismo

**Evidências:**
- [Resposta 1 - Código correto](../evidencias/exemplo/exemplo.png)
- [Resposta 2 - Código com erro](../evidencias/exemplo/exemplo.png)
- [Resposta 3 - Resultado inconsistente](../evidencias/exemplo/exemplo.png)

**Recomendação:** sugestão de melhoria.

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

## Achado 4: Aumento de Custo Computacional e Latência em Entradas Longas

**Nível de Severidade:** Baixa

**Descrição:** Durante a execução do caso de teste CT-08 na formulação longa e composta (envolvendo múltiplas sub-perguntas detalhadas sobre o auxílio home office), o sistema exigiu uma saída extensa dividida em 3 capturas (`ct-08-01-longa`, `ct-08-02-longa` e `ct-08-03-longa`). Embora o conteúdo retornado estivesse correto e completo, observou-se tempo de resposta sensivelmente maior e consumo elevado de tokens de entrada e saída.

**Impacto:** Impacta a eficiência de desempenho e a experiência do usuário devido ao aumento na latência de geração. Em cenários de produção com múltiplos usuários concorrentes, respostas demasiadamente prolixas aumentam o custo computacional da API e a probabilidade de saturação da janela de contexto.

**Categoria Relacionada:** Eficiência de Desempenho, Usabilidade

**Evidência:**
- [Screenshot da resposta longa - Parte 1](../evidencias/casos-de-teste/ct-08-01-longa.png)
- [Screenshot da resposta longa - Parte 2](../evidencias/casos-de-teste/ct-08-02-longa.png)
- [Screenshot da resposta longa - Parte 3](../evidencias/casos-de-teste/ct-08-03-longa.png)
- [Documento original](../evidencias/casos-de-teste/Politica-Beneficios.pdf)
- [Caso de Teste 8 - Robustez a Variações de Extensão da Entrada](06-casos-teste.md#caso-de-teste-8-robustez-a-variações-de-extensão-da-entrada-curta-vs-longa)

**Recomendação:** Avaliar a implementação de técnicas de decomposição de consultas (*Query Decomposition*) ou definir limites de concisão e sumarização no prompt do sistema, orientando o agente a estruturar saídas diretas em tópicos executivos quando exposto a entradas densas.

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
