# Ficha Inicial do Projeto

## Identificação

- Nome do Projeto: AnythingLLM
- URL: https://github.com/MintplexLabs/anything-llm
- Organização: Mintplex Labs
- Licença: MIT

## Contexto de Avaliação

- Última Data de Acesso: 16/09/2026
- Release: v1.16.1

## Aplicação

- Modelo/Provedor: Compatível com múltiplos: OpenAI (GPT-4, GPT-3.5), Anthropic (Claude), Local (LLaMA, Mistral), Google (Gemini) 
- Finalidade: Plataforma de RAG (Retrieval-Augmented Generation) que permite criar assistentes de IA personalizados com capacidade de consultar documentos, fontes externas e bases de conhecimento próprias. Integra LLMs com gerenciamento de fontes e privacidade.

## Público e Domínio

Usuários-Alvo:
- Empresas integrando IA em workflows internos
- Desenvolvedores criando assistentes customizados
- Profissionais de conhecimento (RH, legal, suporte)
- Organizações com dados sensíveis que precisam privacy-first
- Equipes que desejam controlar modelos e dados localmente

Domínio de Aplicação:
- Retrieval-Augmented Generation (RAG)
- Gerenciamento de conhecimento
- Assistentes de IA corporativos
- Processamento de documentos
- Integração de LLMs privados

## Dados

Entrada: 
- Documentos (PDF, DOCX, TXT, Markdown, etc)
- URLs web
- Bases de conhecimento estruturadas
- Prompts de usuários
- Configurações de fontes

Processamento: 
- Indexação de documentos em base vetorial (embeddings)
- Recuperação de contexto relevante (RAG)
- Augmentação de prompts com documentos
- Passagem de informações ao LLM selecionado

Saída: 
- Respostas de IA fundamentadas em fontes documentais
- Referências aos documentos consultados
- Histórico de conversas
- Logs de transações

Fonte de Dados: 
- Uploads de usuários
- Web scraping
- Integrações com APIs externas
- Bases de dados corporativas

## Escopo da Avaliação

Recorte Avaliado: Sistema de RAG e gerenciamento de fontes, com foco em privacidade e rastreabilidade

Inclui:
- Upload e indexação de documentos
- Recuperação de contexto (busca vetorial)
- Augmentação de prompts com fontes
- Indicação de referências em respostas
- Proteção de dados pessoais em logs
- Gerenciamento de permissões de acesso

Exclui:
- Interface de usuário (UI/UX)
- Performance em escala de 10000+ documentos
- Integração com sistemas legados específicos
- Análise de código-fonte profunda (segurança)
- Benchmarks contra concorrentes
- Deploy em produção em nuvem pública

---

[Clique aqui para voltar ao início](/README.md)