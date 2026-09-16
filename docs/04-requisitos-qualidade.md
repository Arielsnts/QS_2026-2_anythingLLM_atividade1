# Requisitos de Qualidade

## Introdução

Este documento apresenta os requisitos de qualidade definidos para a avaliação do AnythingLLM, considerando o recorte de **RAG, fontes, permissões e privacidade**.

Os requisitos têm como objetivo estabelecer critérios verificáveis para avaliar a qualidade da aplicação, permitindo posteriormente a realização de testes e a coleta de evidências.

A especificação considera aspectos relacionados à adequação funcional, confiabilidade, rastreabilidade, segurança e privacidade, características relevantes para o contexto de utilização do AnythingLLM.

---

## Requisitos de qualidade

Os requisitos foram definidos a partir das funcionalidades e dos riscos relacionados ao uso do AnythingLLM como aplicação de IA generativa baseada na utilização de documentos e recuperação de informações.

A primeira parte (RQ-01 a RQ-05) dos requisitos é de responsabilidade de Fernanda Farias, enquanto os demais (RQ-06 a RQ-010) requisitos foram definidos por João Lucas.

### Requisitos

| **ID** | **Requisito** | **Categoria** | **Prioridade** | **Critérios de aceitação** | **Evidência**
| --- | --- | --- | --- | --- | --- |
| RQ-01 | O sistema deve apresentar as fontes utilizadas para fundamentar respostas geradas a partir dos documentos disponíveis no workspace. | Rastreabilidade | Alta | Para uma consulta cuja resposta dependa de informações presentes nos documentos, deve ser possível identificar a fonte utilizada. | Captura da resposta e da fonte apresentada.
| RQ-02 | O sistema deve recuperar informações relevantes dos documentos disponíveis no workspace para responder consultas relacionadas ao seu conteúdo. | Adequação funcional | Alta | Ao realizar uma consulta sobre uma informação presente nos documentos, o sistema deve retornar uma resposta relacionada ao conteúdo disponível. | Documento utilizado, prompt e resposta gerada
| RQ-03 | O sistema deve indicar quando não houver informações suficientes nos documentos disponíveis para responder à consulta. | Confiabilidade | Alta | Quando a informação solicitada não estiver disponível nas fontes recuperadas, o sistema não deve apresentá-la como fundamentada pelos documentos. | Prompt, resposta gerada e fontes apresentadas
| RQ-04 | O sistema deve restringir o acesso às informações disponibilizadas em um workspace aos usuários autorizados. | Privacidade | Alta | Um usuário sem autorização para acessar determinado workspace não deve conseguir consultar ou recuperar suas informações. | Configuração de permissões e resultado do teste de acesso
| RQ-05 | O sistema deve manter o isolamento das informações entre diferentes workspaces de acordo com as permissões configuradas. | Segurança | Alta | Uma consulta realizada em um workspace não deve recuperar informações provenientes de outro workspace ao qual o usuário não possui autorização. | Configuração de dois workspaces, permissões e resultado do teste
| RQ-06 | O sistema deve retornar a resposta gerada para uma consulta padrão dentro de um limite de tempo aceitável. | Desempenho | Média | Para uma consulta textual padrão em um workspace indexado, o tempo de resposta completo não deve exceder um limite estipulado em condições normais de infraestrutura. | Log de tempo de execução da requisição e registro de timestamp.
| RQ-07 | A interface de chat do sistema deve fornecer feedback visual claro durante o processamento e a geração da resposta. | Interação | Média | Enquanto o modelo estiver processando a consulta, a interface deve exibir um indicador visual de carregamento para informar o usuário sobre o status da operação. | Captura de tela ou gravação da interface exibindo o indicador de carregamento.
| RQ-08 | O sistema deve permitir a alteração do provedor de modelo de linguagem (LLM) e de embeddings sem perda de dados dos workspaces. | Flexibilidade | Média | O administrador deve conseguir alterar o provedor de LLM nas configurações gerais do sistema sem que os documentos indexados ou históricos de chat sejam corrompidos. | Tela de configurações alterada e verificação do funcionamento pós-troca do provedor.
| RQ-09 | O sistema deve tratar falhas temporárias de conexão com o provedor de LLM externo de forma estável. | Robustez | Alta | Em caso de perda de conexão com a API do provedor de LLM, o sistema deve exibir uma mensagem de erro amigável ao usuário sem interromper o funcionamento geral da aplicação. | Simulação de falha de rede, mensagem de erro exibida na interface e logs do servidor.
| RQ-10 | O sistema deve disponibilizar mecanismos para que o usuário avalie a utilidade ou precisão das respostas geradas. | Supervisão Humana | Baixa | O usuário deve ter a opção de registrar feedback qualitativo (ex: botões de aprovação/revisão) sobre as respostas geradas pelo modelo no workspace. | Captura de tela dos botões de feedback na interface de chat e registro da interação.

---

## Conclusão

Os 10 requisitos apresentados estabelecem critérios de qualidade abrangentes para a avaliação do AnythingLLM, contemplando desde a precisão do RAG e segurança de dados até aspectos de desempenho, robustez, flexibilidade e experiência do usuário.

A verificação desses requisitos será realizada por meio de casos de teste e evidências coletadas durante a avaliação da aplicação.

---

[Clique aqui para voltar ao início](/README.md) 
