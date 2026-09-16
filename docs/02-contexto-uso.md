# Contexto de uso e riscos

## Introdução

Este documento apresenta a análise do AnythingLLM quanto à sua finalidade, usuários, dados utilizados, supervisão humana, decisões apoiadas, erros aceitáveis e inaceitáveis, limitações e principais riscos relacionados ao seu uso.

---

## Contexto de uso

### Finalidade

O AnythingLLM é uma aplicação de inteligência artificial que permite interagir com modelos de linguagem e consultar documentos como fonte de contexto. Entre suas funcionalidades estão a interação com documentos, o uso de agentes de IA e a automação de fluxos de trabalho.

### Usuários

O sistema pode ser utilizado individualmente ou em ambientes multiusuário. Nesses ambientes, os usuários podem utilizar diferentes workspaces e recursos de acordo com as configurações de acesso definidas.

### Dados utilizados

O AnythingLLM utiliza documentos enviados pelos usuários e seus respectivos metadados, além de representações vetoriais dos documentos. Também são utilizados dados relacionados aos usuários e às interações realizadas, como prompts, respostas, histórico de conversas, workspaces, threads, sessões e avaliações.

Em instalações self-hosted, esses dados podem permanecer na infraestrutura do usuário. Porém, quando são utilizadas integrações externas, determinados dados podem ser enviados aos respectivos provedores.

### Supervisão humana

O sistema disponibiliza recursos que permitem acompanhar e avaliar as respostas, como citações das fontes utilizadas, visualização dos trechos recuperados e feedback sobre as respostas. Esses recursos auxiliam na conferência das informações, mas não garantem sua correção.

Por isso, a supervisão humana é necessária, principalmente quando as respostas forem utilizadas em atividades relevantes ou para apoiar decisões.

### Decisões apoiadas

O AnythingLLM pode auxiliar atividades que dependem da consulta e interpretação de informações, como localização de informações relevantes, consulta de procedimentos e interpretação de documentos.

As respostas podem apoiar ações ou decisões do usuário, mas não devem ser consideradas como autoridade final. Informações utilizadas em decisões relevantes devem ser verificadas pelo usuário.

### Erros aceitáveis e inaceitáveis

A aceitabilidade dos erros depende de seu impacto. Pequenas imprecisões ou respostas incompletas podem ser toleradas em situações de baixo impacto, quando podem ser facilmente verificadas ou corrigidas.

Já respostas incorretas ou não fundamentadas, resultados analíticos incorretos e erros que possam comprometer a privacidade dos usuários são considerados inaceitáveis quando podem influenciar conclusões, decisões ou causar exposição de informações.

### Limitações

A qualidade das respostas pode variar de acordo com o modelo de linguagem utilizado, os documentos fornecidos, as configurações adotadas e as integrações externas. Dessa forma, o sistema não garante que todas as informações geradas sejam corretas ou adequadas ao contexto de uso.

---

## Riscos

Os principais riscos identificados estão relacionados à **confiabilidade das respostas, recuperação de informações, análise de dados, privacidade, disponibilidade e dependência de serviços externos**.

O uso de modelos de linguagem pode resultar em respostas incorretas ou inventadas. Da mesma forma, documentos inadequados ou problemas na recuperação das informações podem comprometer a qualidade das respostas e de suas fontes.

Também existe risco relacionado à análise de dados, pois resultados incorretos podem levar a conclusões inadequadas quando utilizados sem verificação. Em ambientes multiusuário, falhas ou limitações no controle de acesso podem resultar na exposição de documentos ou conversas de outros usuários.

Além disso, a utilização de integrações e serviços externos pode causar problemas de disponibilidade quando esses serviços apresentarem falhas, alterações ou limitações.

De modo geral, os riscos identificados são tratados de forma distribuída no repositório, principalmente por meio de Issues, Pull Requests, commits e correções. Não foi identificada uma estrutura formal de registro de riscos com avaliação prévia de probabilidade, impacto e prioridade.

---

## Conclusão

O AnythingLLM apresenta diferentes possibilidades de uso para consulta e interpretação de informações por meio de documentos, modelos de linguagem e agentes de IA. Entretanto, seu uso envolve limitações e riscos relacionados principalmente à precisão das respostas, aos dados utilizados, à privacidade e à dependência de serviços externos.

Por esse motivo, a utilização do sistema deve considerar suas limitações e manter a supervisão humana, especialmente quando as informações geradas forem utilizadas para apoiar decisões relevantes.

---

[Clique aqui para voltar ao início](/README.md)