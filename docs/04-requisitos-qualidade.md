# Requisitos de Qualidade

## Introdução

Este documento apresenta os requisitos de qualidade definidos para a avaliação do AnythingLLM, considerando o recorte de **RAG, fontes, permissões e privacidade**.

Os requisitos têm como objetivo estabelecer critérios verificáveis para avaliar a qualidade da aplicação, permitindo posteriormente a realização de testes e a coleta de evidências.

A especificação considera aspectos relacionados à adequação funcional, confiabilidade, rastreabilidade, segurança e privacidade, características relevantes para o contexto de utilização do AnythingLLM.

---

## Requisitos de qualidade

Os requisitos foram definidos a partir das funcionalidades e dos riscos relacionados ao uso do AnythingLLM como aplicação de IA generativa baseada na utilização de documentos e recuperação de informações.

A primeira parte dos requisitos é de responsabilidade de Fernanda Farias, enquanto os demais requisitos serão definidos por João Lucas.

### Requisitos - Fernanda Farias

| **ID** | **Requisito** | **Categoria** | **Prioridade** | **Critérios de aceitação** | **Evidência**
| --- | --- | --- | --- | --- | --- |
| RQ-01 | O sistema deve apresentar as fontes utilizadas para fundamentar respostas geradas a partir dos documentos disponíveis no workspace. | Rastreabilidade | Alta | Para uma consulta cuja resposta dependa de informações presentes nos documentos, deve ser possível identificar a fonte utilizada. | Captura da resposta e da fonte apresentada.
| RQ-02 | O sistema deve recuperar informações relevantes dos documentos disponíveis no workspace para responder consultas relacionadas ao seu conteúdo. | Adequação funcional | Alta | Ao realizar uma consulta sobre uma informação presente nos documentos, o sistema deve retornar uma resposta relacionada ao conteúdo disponível. | Documento utilizado, prompt e resposta gerada
| RQ-03 | O sistema deve indicar quando não houver informações suficientes nos documentos disponíveis para responder à consulta. | Confiabilidade | Alta | Quando a informação solicitada não estiver disponível nas fontes recuperadas, o sistema não deve apresentá-la como fundamentada pelos documentos. | Prompt, resposta gerada e fontes apresentadas
| RQ-04 | O sistema deve restringir o acesso às informações disponibilizadas em um workspace aos usuários autorizados. | Privacidade | Alta | Um usuário sem autorização para acessar determinado workspace não deve conseguir consultar ou recuperar suas informações. | Configuração de permissões e resultado do teste de acesso
| RQ-05 | O sistema deve manter o isolamento das informações entre diferentes workspaces de acordo com as permissões configuradas. | Segurança | Alta | Uma consulta realizada em um workspace não deve recuperar informações provenientes de outro workspace ao qual o usuário não possui autorização. | Configuração de dois workspaces, permissões e resultado do teste

---

## Evidências

As evidências dos requisitos serão coletadas durante a avaliação do AnythingLLM e armazenadas no diretório de evidências do projeto.

Para cada requisito, serão utilizadas evidências compatíveis com o método de verificação, como capturas da interface, prompts, respostas geradas, fontes apresentadas, configurações e resultados dos testes.

Exemplo de referência:

Captura da interface: [Clique aqui para visualizar](/teste) 

As evidências serão adicionadas após a execução dos testes correspondentes aos requisitos.

---

## Conclusão

Os cinco requisitos apresentados estabelecem critérios de qualidade relacionados aos principais aspectos do recorte definido para a avaliação do AnythingLLM.

Os requisitos priorizam a capacidade de recuperação de informações, a identificação das fontes utilizadas, a confiabilidade das respostas e o controle de acesso às informações disponibilizadas nos workspaces.

A verificação desses requisitos será realizada por meio de casos de teste e evidências coletadas durante a avaliação da aplicação.

[Clique aqui para voltar ao início](/README.md) 
