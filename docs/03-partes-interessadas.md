# Partes Interessadas

## Introdução

Este documento apresenta as principais partes interessadas envolvidas no contexto de uso e avaliação do AnythingLLM.

A análise considera o recorte definido pela equipe, com foco em RAG, rastreabilidade das fontes, permissões e privacidade. Para cada parte interessada são descritos seu objetivo, expectativa em relação ao sistema, possíveis danos decorrentes de falhas, evidências desejadas e responsabilidades.

---

## Identificação das Partes Interessadas

Foram identificadas cinco partes interessadas relevantes para a avaliação da qualidade do AnythingLLM.

### Usuário final

O usuário final utiliza o AnythingLLM para realizar perguntas e obter informações a partir dos documentos disponibilizados no sistema.

Espera-se que as respostas sejam claras, relevantes e fundamentadas nas fontes utilizadas pelo mecanismo de RAG. Caso o sistema apresente informações incorretas, inventadas ou sem suporte documental, o usuário pode tomar decisões com base em informações inadequadas.

Como evidência da qualidade, podem ser utilizadas respostas geradas pelo sistema, fontes apresentadas e capturas de tela dos testes realizados.

### Administrador do sistema

O administrador é responsável pela configuração do ambiente, gerenciamento de usuários, documentos, workspaces e permissões de acesso.

Sua expectativa é que o sistema permita controlar adequadamente quem pode acessar documentos e funcionalidades. Falhas nessa área podem resultar em acesso não autorizado ou exposição de informações privadas.

As principais evidências esperadas incluem configurações de permissões, testes de controle de acesso e registros que demonstrem o bloqueio de usuários não autorizados.

### Desenvolvedores e mantenedores do AnythingLLM

Os desenvolvedores e mantenedores são responsáveis pela evolução, correção e manutenção do software.

Espera-se que o sistema apresente comportamento confiável, seguro e consistente, especialmente nos mecanismos relacionados a recuperação de informações, geração de respostas e apresentação de fontes.

Falhas no software podem provocar respostas incorretas, vulnerabilidades, problemas de privacidade ou perda de confiança dos usuários.

As evidências desejadas incluem resultados de testes, logs, registros de falhas, issues e informações relacionadas às versões avaliadas.

### Organização usuária do AnythingLLM

Uma organização pode utilizar o AnythingLLM para consultar informações presentes em documentos internos e apoiar atividades de seus colaboradores.

Espera-se que o sistema permita a utilização de IA generativa preservando a segurança, a privacidade e a confiabilidade das informações.

Entre os possíveis danos estão a exposição de informações confidenciais, respostas incorretas utilizadas em processos internos e uso inadequado dos dados armazenados.

As evidências esperadas incluem testes de segurança, privacidade, confiabilidade, rastreabilidade e controle de acesso.

### Responsável pelos dados e documentos

O responsável pelos dados e documentos deve garantir que as fontes disponibilizadas ao AnythingLLM sejam adequadas, corretas e atualizadas.

Sua expectativa é que o sistema utilize corretamente os documentos fornecidos e permita identificar a origem das informações utilizadas nas respostas.

Documentos incorretos ou desatualizados podem levar o sistema a produzir respostas inadequadas mesmo quando o mecanismo de recuperação funciona corretamente.

As evidências desejadas incluem os documentos originais utilizados nos testes, versões dos arquivos, fontes associadas às respostas e registros da recuperação de informações.

---

## Tabela de Partes Interessadas

| **ID** | **Parte interessada** | **Objetivo** | **Expectativa** | **Possível dano** | **Evidência desejada** | **Responsabilidade** |
| --- | --- | --- | --- | --- | --- | --- |
| PI-01 | Usuário final | Obter respostas úteis a partir dos documentos inseridos no sistema. | Receber respostas claras, corretas e fundamentadas em fontes. | Tomar decisões com base em respostas incorretas ou não fundamentadas. | Respostas, fontes apresentadas e capturas de tela. | Formular consultas adequadas e verificar informações importantes antes de utilizá-las. |
| PI-02 | Administrador do sistema | Gerenciar workspaces, usuários, documentos e permissões. | Garantir que somente usuários autorizados tenham acesso aos dados e funcionalidades. | Exposição de documentos privados ou acesso indevido a informações. | Configurações de acesso, testes de permissão e registros do sistema. | Configurar usuários, permissões e mecanismos de segurança. |
| PI-03 | Desenvolvedores e mantenedores | Manter, corrigir e evoluir o AnythingLLM. | Garantir funcionamento confiável, seguro e rastreável. | Bugs, vulnerabilidades, respostas incorretas ou falhas no mecanismo de RAG. | Casos de teste, logs, issues e resultados de avaliação. | Corrigir defeitos, manter o código e implementar melhorias. |
| PI-04 | Organização usuária | Utilizar IA generativa para consultar informações e apoiar atividades internas. | Utilizar uma solução confiável, segura e que preserve informações confidenciais. | Vazamento de informações, respostas incorretas ou perda de confiança na ferramenta. | Testes de privacidade, segurança, confiabilidade e rastreabilidade. | Definir políticas de uso e controlar quais dados podem ser utilizados. |
| PI-05 | Responsável pelos dados e documentos | Disponibilizar fontes adequadas para utilização pelo mecanismo de RAG. | Garantir que as informações utilizadas sejam corretas, atualizadas e identificáveis. | Respostas inadequadas causadas por documentos incorretos ou desatualizados. | Documentos originais, versão dos arquivos, fontes e registros de recuperação. | Selecionar, revisar e manter atualizados os documentos utilizados pelo sistema. |

---

## Conclusão

A identificação das partes interessadas demonstra que a qualidade do AnythingLLM não depende apenas das respostas produzidas pelo modelo de IA.

Também devem ser considerados aspectos relacionados à qualidade dos documentos utilizados, gerenciamento de permissões, privacidade, segurança, manutenção do software e uso responsável das informações.

Os stakeholders identificados servirão como referência para a definição dos requisitos de qualidade e dos casos de teste utilizados nas próximas etapas da avaliação.
