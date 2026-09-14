# Casos de Teste

## Introdução

Este documento apresenta os casos de teste definidos para a avaliação do AnythingLLM, com foco no recorte de **RAG, fontes, permissões e privacidade**.

Os casos de teste foram projetados para validar o atendimento aos requisitos de qualidade definidos em [Requisitos de Qualidade](04-requisitos-qualidade.md) e as características aplicáveis da ISO/IEC 25010:2023.

Cada caso de teste especifica uma entrada controlada, as condições esperadas, o resultado esperado e a evidência que será coletada. Os testes abordam cenários normais, situações de borda, dados sensíveis e comportamentos críticos para confiabilidade e segurança.

A avaliação também inclui análise de variabilidade e não determinismo, documentada separadamente em [Variabilidade e Não Determinismo](07-variabilidade.md).

---

## Metodologia

Os testes são executados com base em critérios de aceitação claros. Para cada caso de teste, o resultado é classificado como:

- **A (Aprovado):** O sistema se comportou conforme esperado, atendendo ao critério de aceitação
- **P (Parcial):** O sistema atendeu parcialmente, com desvios menores ou comportamentos não ideais
- **R (Reprovado):** O sistema não atendeu ao critério de aceitação

---

## Caso de Teste 1: Recuperação de Informação com Indicação de Fonte

**ID:** CT-01

**Tipo:** Caso esperado (Happy Path)

**Relacionado a:**
- Requisito: [RQ-01 - Indicar fontes](04-requisitos-qualidade.md#rq-01)
- Característica ISO: Adequação funcional, Rastreabilidade

**Descrição:** Validar que o sistema recupera informação relevante de um documento e apresenta a fonte corretamente.

**Entrada:** 
Prompt: "Quais são os principais objetivos da empresa conforme o documento de missão?"
Documento: [Manual-Organizacional.pdf](../evidencias/casos-de-teste/Manual-Organizacional.pdf) contendo seção "Missão e Objetivos"

**Condição:** 
- Usuário autenticado no workspace
- Documento indexado e disponível
- Prompt refere-se a informação presente no documento
- Primeira execução (sem histórico prévio)

**Esperado:** 
A resposta deve incluir informações extraídas do documento e apresentar uma referência clara à fonte (ex: "Conforme Manual-Organizacional.pdf, página 3")

**Resultado Obtido:** 
[Será preenchido após execução]

**Evidência:** 
- [Screenshot da resposta](../evidencias/casos-teste/ct-01/resposta-captura.png)
- [Prompt exato utilizado](../evidencias/casos-teste/ct-01/prompt.txt)
- [Documento original](../evidencias/casos-teste/ct-01/Manual-Organizacional.pdf)
- [Identificação da fonte indicada](../evidencias/casos-teste/ct-01/fonte-indicada.txt)

**Status:** 
[A / P / R]

**Observações:** 
Teste fundamental para validar rastreabilidade. Fonte deve ser identificável e recuperável.

---

## Caso de Teste 2: Indicação de Insuficiência de Informação

**ID:** CT-02

**Tipo:** Falta de informação

**Relacionado a:**
- Requisito: [RQ-03 - Indicar insuficiência](04-requisitos-qualidade.md#rq-03)
- Característica ISO: Confiabilidade, Adequação funcional

**Descrição:** Validar que o sistema não afirma como fundamentadas as informações não presentes nos documentos.

**Entrada:** 
Prompt: "Qual é o plano de expansão internacional da empresa para 2027?"
Documento: [Manual-Organizacional.pdf](../evidencias/casos-de-teste/Manual-Organizacional.pdf) contendo apenas informações até 2024

**Condição:** 
- Usuário autenticado no workspace
- Documento indexado e disponível
- Prompt solicita informação não presente nos documentos
- Workspace contém apenas este documento

**Esperado:** 
O sistema deve indicar que não encontrou informação sobre plano de expansão 2027 nos documentos disponíveis. Exemplos aceitáveis:
- "Não encontrei informação sobre expansão em 2027 nos documentos disponíveis"
- "Esta informação não está presente nas fontes consultadas"
- O sistema não deve afirmar fatos sobre 2027 como se fossem documentados

**Resultado Obtido:** 
[Será preenchido após execução]

**Evidência:** 
- [Screenshot da resposta](../evidencias/casos-teste/ct-02/resposta-captura.png)
- [Prompt utilizado](../evidencias/casos-teste/ct-02/prompt.txt)
- [Indicação de insuficiência](../evidencias/casos-teste/ct-02/mensagem-insuficiencia.txt)
- [Log de busca vetorial](../evidencias/casos-teste/ct-02/log-busca.txt)

**Status:** 
[A / P / R]

**Observações:** 
Crítico para confiabilidade. Alucinação é risco alto se sistema inventar informações sobre 2027.

---

## Caso de Teste 3: Isolamento de Informações entre Workspaces

**ID:** CT-03

**Tipo:** Segurança e isolamento

**Relacionado a:**
- Requisito: [RQ-04 - Restringir acesso](04-requisitos-qualidade.md#rq-04), [RQ-05 - Isolamento entre workspaces](04-requisitos-qualidade.md#rq-05)
- Característica ISO: Segurança, Privacidade

**Descrição:** Validar que informações de um workspace não são recuperadas em consultas de outro workspace.

**Entrada:** 
- Workspace A: Contém [Salarios-Confidencial.pdf](../evidencias/casos-de-teste/Salarios-Confidencial.pdf) (dado sensível)
- Workspace B: Contém apenas [Manual-Organizacional.pdf](../evidencias/casos-de-teste/Manual-Organizacional.pdf)
- Prompt em Workspace B: "Qual é o salário do gerente de vendas?"
- Usuário: Autenticado em Workspace B apenas (sem acesso a Workspace A)

**Condição:** 
- Dois workspaces separados criados
- Dados sensíveis no Workspace A
- Usuário autenticado apenas em Workspace B
- Documento sensível não deve estar indexado em Workspace B
- Ambos workspaces usando mesmo LLM provider

**Esperado:** 
Workspace B deve retornar "Informação não encontrada nos documentos disponíveis" ou similar. Não deve retornar dados de salários mesmo que existam em Workspace A.

**Resultado Obtido:** 
[Será preenchido após execução]

**Evidência:** 
- [Screenshot de acesso negado ou "não encontrado"](../evidencias/casos-teste/ct-03/resposta-captura.png)
- [Configuração de permissões do Workspace A](../evidencias/casos-teste/ct-03/config-workspace-a.txt)
- [Configuração de permissões do Workspace B](../evidencias/casos-teste/ct-03/config-workspace-b.png)
- [Logs de busca mostrando isolamento](../evidencias/casos-teste/ct-03/log-isolamento.txt)
- [Prompt utilizado](../evidencias/casos-teste/ct-03/prompt.txt)

**Status:** 
[A / P / R]

**Observações:** 
Crítico para privacidade e segurança. Vazamento entre workspaces é risco crítico para dados corporativos e sensíveis.

---


## Caso de Teste 4: Exposição de Dados Sensíveis em Logs

**ID:** CT-04

**Tipo:** Dado sensível

**Relacionado a:**
- Requisito: [RQ-04 - Restringir acesso](04-requisitos-qualidade.md#rq-04)
- Característica ISO: Privacidade, Segurança

**Descrição:** Validar que dados pessoais inseridos em prompts não são expostos em logs públicos ou acessíveis.

**Entrada:** 
Prompt: "Qual é a política de benefícios para o funcionário João Silva, CPF 123.456.789-00, email joao@empresa.com?"
Documento: [Politica-Beneficios.pdf](../evidencias/casos-de-teste/Politica-Beneficios.pdf) contendo política geral

**Condição:** 
- Usuário autenticado no workspace
- Documento indexado e disponível
- Prompt contém dados pessoais identificáveis (nome, CPF, email)
- Sistema registra logs de requisições
- Acesso aos logs sem autenticação adicional

**Esperado:** 
Os logs não devem exibir dados sensíveis (CPF, email pessoal, nome completo). Exemplos aceitáveis:
- Dados são mascarados nos logs: "CPF: ***-***-**00"
- Dados sensíveis não são persistidos: apenas hash ou ID de usuário
- Logs requerem autenticação e autorização para acesso
- Resposta inclui política, mas não expõe dados pessoais

**Resultado Obtido:** 
[Será preenchido após execução]

**Evidência:** 
- [Screenshot da resposta](../evidencias/casos-teste/ct-04/resposta-captura.png)
- [Prompt contendo dados sensíveis](../evidencias/casos-teste/ct-04/prompt-sensivel.txt)
- [Print dos logs do sistema](../evidencias/casos-teste/ct-04/logs-sistema.txt)
- [Verificação de sanitização](../evidencias/casos-teste/ct-04/dados-expostos.txt)
- [Configuração de retenção de logs](../evidencias/casos-teste/ct-04/config-logs.txt)

**Status:** 
[A / P / R]

**Observações:** 
Crítico para conformidade com LGPD/GDPR. Vazamento de dados pessoais é risco crítico e pode resultar em multas regulatórias.

---

## Caso de Teste 5: Reformulação da Mesma Consulta com Variações Linguísticas

**ID:** CT-05

**Tipo:** Reformulação

**Relacionado a:**
- Requisito: [RQ-02 - Recuperação de informações](04-requisitos-qualidade.md#rq-02)
- Característica ISO: Adequação funcional, Confiabilidade

**Descrição:** Validar que o sistema consegue recuperar as mesmas informações mesmo quando a consulta é formulada de maneiras diferentes.

**Entrada:** 
Documento: [Politica-Beneficios.pdf](../evidencias/casos-de-teste/Politica-Beneficios.pdf)

Três variações do mesmo prompt:
- Versão A: "Quais são os benefícios oferecidos aos funcionários?"
- Versão B: "Que vantagens e auxílios a empresa concede aos colaboradores?"
- Versão C: "Descreva o pacote de benefícios corporativos disponível"

**Condição:** 
- Mesmo documento indexado em todas as execuções
- Mesmo workspace e usuário
- Prompts diferentes mas com mesma intenção semântica
- Execuções sequenciais com intervalo mínimo

**Esperado:** 
As três variações devem recuperar informações essencialmente iguais, com as mesmas fontes indicadas. Respostas podem ter estrutura ou redação diferentes, mas conteúdo factual deve ser consistente.

**Resultado Obtido:** 
[Será preenchido após execução]

**Evidência:** 
- [Resposta Versão A](../evidencias/casos-teste/ct-05/resposta-versao-a.png)
- [Resposta Versão B](../evidencias/casos-teste/ct-05/resposta-versao-b.png)
- [Resposta Versão C](../evidencias/casos-teste/ct-05/resposta-versao-c.png)
- [Análise comparativa de fontes](../evidencias/casos-teste/ct-05/fontes-comparadas.txt)
- [Documento original](../evidencias/casos-teste/ct-05/Politica-Beneficios.pdf)

**Status:** 
[A / P / R]

**Observações:** 
Testa capacidade de compreensão semântica e robustez de recuperação. Variações inaceitáveis podem indicar frágil indexação ou embedding inadequado.

---

### Análise de Variabilidade

Os três casos de teste acima também serão executados múltiplas vezes para análise de variabilidade e não determinismo. Consulte [Variabilidade e Não Determinismo](07-variabilidade.md) para mais detalhes.

---

[Clique aqui para voltar ao início](/README.md)