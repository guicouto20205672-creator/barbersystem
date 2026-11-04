# ADR-003 — Topologia Corteza para isolamento por tenant

- **Status:** proposta para prova de conceito; não aprovada para produção.
- **Data:** 2026-11-04

## Contexto

O requisito do BarberSystem determina um banco de dados independente para cada empresa. A configuração de servidor Corteza documenta um único parâmetro de conexão de datastore (`DB_DSN`) por instância de servidor.

## Decisão provisória

A prova de conceito local utilizará uma instância Corteza ligada a um PostgreSQL dedicado, representando somente um ambiente de desenvolvimento/uma empresa.

Para cumprir banco independente por tenant em produção, a hipótese inicial a validar é uma instalação lógica isolada por tenant (instância de aplicação e banco próprios), administrada por um plano de controle SaaS separado. Não assumir que uma única instância Corteza compartilha dinamicamente conexões independentes por tenant.

## Plano de validação

1. Confirmar em teste como Corteza trata autenticação, usuários, permissões e APIs em uma instalação.
2. Executar duas instalações de teste independentes com bancos distintos.
3. Demonstrar que credenciais, sessões, arquivos, automações e dados de uma instalação não alcançam a outra.
4. Medir recursos e custo operacional por instalação.
5. Validar provisionamento, atualização, backup e restauração automatizados.
6. Definir como o plano de controle roteia o domínio e a sessão para a instalação correta.
7. Revisar isolamento de arquivos e serviços auxiliares, não apenas do PostgreSQL.

## Riscos

- Uma instância por tenant aumenta consumo de recursos e esforço de atualização.
- O Corredor e outros serviços auxiliares podem exigir configuração e isolamento por instalação.
- O provisionamento precisa evitar vazamento de credenciais.
- Uma atualização em lote precisa ser controlada e reversível.
- A documentação da configuração de servidor mostra `DB_DSN` como conexão do datastore; não foi identificada nesta etapa uma configuração nativa documentada para alternar banco por tenant em uma única instância.

## Critério de aprovação

A topologia só será aprovada após testes práticos de isolamento, provisionamento, migração, backup, restauração e custo. Se a hipótese de uma instalação por tenant não for sustentável, reavaliar o requisito e alternativas antes de iniciar a implementação comercial.

## Referências oficiais

- Configuração do servidor: https://docs.cortezaproject.org/corteza-docs/2026.9/devops-guide/references/configuration/server.html
- Exemplo local Docker Compose: https://docs.cortezaproject.org/corteza-docs/2026.9/integrator-guide/automation/automation-scripts/examples/local-setup.html
- Atualização para 2026.9: https://docs.cortezaproject.org/corteza-docs/2026.9/devops-guide/upgrade/202609.html
