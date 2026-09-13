# Achados da Avaliação

IMPORTANTE: ANTES DE ALTERAR ESSE DOC, VERIFIQUE SE ESTÁ SYNCADO COM O REPO REMOTO

## Introdução

Este documento consolida os achados identificados durante a avaliação de qualidade da aplicação de IA generativa. Cada achado é classificado por nível de severidade e acompanhado de evidências que fundamentam a análise.

Os achados são resultado da execução de casos de teste, análise de variabilidade e aplicação dos critérios ISO/IEC 25010:2023 documentados nos relatórios técnicos anteriores.

---

## Achado 1: Exemplo de achado

**Nível de Severidade:** Alta

**Descrição:** A aplicação não indica as fontes utilizadas para fundamentar respostas em consultas documentais. Usuários recebem informações sem poder verificar a origem ou validar a precisão das afirmações.

**Impacto:** Reduz confiabilidade e impossibilita auditoria de respostas. Usuários não conseguem validar informações críticas ou rastrear dados originais.

**Categoria Relacionada:** Rastreabilidade, Confiabilidade

**Requisito Violado:** [RQ-01 - Indicar fontes em respostas documentais](04-requisitos-qualidade.md#rq-01)

**Evidência:** [Captura de resposta sem fontes](../evidencias/exemplo/exemplo.png)

**Recomendação:** sugestão de melhoria.

---

## Achado n: Exemplo de achado

**Nível de Severidade:** Muito Alta

**Descrição:** Execuções idênticas do mesmo prompt produzem respostas semanticamente diferentes. Em um caso, a aplicação retornou código correto; em outro, código com erro lógico. Não há indicação de quando a resposta é derivada de alucinação.

**Impacto:** Impede confiança em respostas técnicas. Usuários não conseguem determinar se a resposta é confiável ou se foi gerada sem fundamentação real.

**Categoria Relacionada:** Confiabilidade, Variabilidade, Não Determinismo

**Requisito Violado:** [RQ-02 - Sinalizar incerteza sem evidência suficiente](04-requisitos-qualidade.md#rq-02)

**Evidências:**
- [Resposta 1 - Código correto](../evidencias/exemplo/exemplo.png)
- [Resposta 2 - Código com erro](../evidencias/exemplo/exemplo.png)
- [Resposta 3 - Resultado inconsistente](../evidencias/exemplo/exemplo.png)

**Recomendação:** sugestão de melhoria.

---

Veja [Plano de Melhoria](02-contexto-uso.md) para consolidação dos achados.

---

[Clique aqui para voltar ao início](/README.md) 