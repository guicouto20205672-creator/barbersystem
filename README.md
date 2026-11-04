# BarberSystem

Plataforma SaaS de gestão para barbearias, com operação web responsiva, agenda, fila de espera inteligente, clientes, equipe, estoque, PDV e gestão financeira.

> **Estado do projeto:** fase inicial de estruturação. Este repositório ainda não contém uma aplicação executável. As decisões técnicas de implantação serão validadas antes da inclusão de serviços, imagens ou configurações de infraestrutura.

## Objetivo

Construir um produto comercial confiável para barbearias pequenas, médias e grandes, com isolamento de dados entre empresas (tenants), experiência premium e operação em computador e celular.

## Escopo planejado da versão 1

- Dashboard gerencial com indicadores financeiros e operacionais.
- Agenda web com disponibilidade e prevenção de conflitos.
- Fila de espera inteligente, com atendimento sequencial e prazo de 5 minutos por oferta.
- Cadastro e relacionamento com clientes (CRM).
- Funcionários, perfis e permissões.
- Serviços e produtos.
- Estoque e movimentações.
- PDV, pagamentos e sessões de caixa.
- Financeiro e relatórios.
- Integração com WhatsApp Business oficial, respeitando políticas e modelos aprovados.
- Administração SaaS e provisionamento de empresas.

## Princípios de arquitetura

1. **Isolamento por empresa:** cada tenant terá banco de dados independente.
2. **Preparação para unidades:** a arquitetura terá entidade de unidade desde o início, mas a V1 operará com uma unidade ativa por empresa.
3. **Segurança no servidor:** permissões e limites de tenant nunca dependerão apenas da interface.
4. **Integridade operacional:** agenda, estoque, vendas, pagamentos e fila devem usar operações transacionais quando necessário.
5. **Responsividade:** experiência adequada para desktop e celular.
6. **Segredos fora do Git:** credenciais, tokens, chaves e dados reais nunca devem ser versionados.

## Documentação

- [Visão geral da arquitetura](docs/arquitetura/overview.md)
- [Escopo funcional da V1](docs/requisitos/escopo-v1.md)
- [Dashboard — especificação BS-UI-001](docs/telas/dashboard.md)
- [ADR-001 — isolamento de dados por tenant](docs/decisoes/ADR-001-isolamento-tenant.md)

## Estado das decisões técnicas

Corteza foi selecionada como plataforma principal a ser avaliada para a solução. Antes de definir imagens Docker, versões, variáveis de ambiente e topologia de implantação, será feita validação na documentação oficial e em um ambiente de teste. Não assumir compatibilidade ou configuração sem teste.

## Desenvolvimento

As etapas serão registradas neste repositório. A primeira entrega prioriza documentação, arquitetura validada e uma base segura; a implementação dos módulos virá em incrementos testáveis.

## Segurança

- Não envie arquivos `.env`, tokens, senhas, chaves privadas, dumps de banco ou dados de clientes.
- Use somente dados fictícios em demonstrações e testes.
- Configure segredos em um gerenciador apropriado no ambiente de implantação.
