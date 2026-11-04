# ADR-001 — Isolamento de dados por tenant

- **Status:** Aceita como requisito arquitetural; implementação pendente.
- **Data:** 2026-11-04

## Contexto

BarberSystem será um SaaS multiempresa. Dados de clientes, funcionários, agenda, vendas, estoque e financeiro de uma barbearia não podem ficar acessíveis a outra.

## Decisão

Cada tenant terá um banco de dados independente. A camada central do SaaS manterá o cadastro e o estado administrativo dos tenants e fará o provisionamento das instalações.

A referência de conexão de cada banco deve ser protegida em um gerenciador de segredos. Credenciais não serão armazenadas no código, no frontend ou no repositório.

## Consequências positivas

- Fronteira de isolamento mais forte entre empresas.
- Possibilidade de backup, restauração e manutenção por tenant.
- Menor risco de consultas operacionais cruzarem dados de empresas.

## Custos e desafios

- Provisionamento e atualização de vários bancos.
- Migrações precisam ser executadas e monitoradas por tenant.
- Backups e restaurações exigem automação e testes.
- Observabilidade, suporte e custos de infraestrutura ficam mais complexos.
- O roteamento de tenant precisa ser seguro e auditável.

## Regras

1. Identificar tenant a partir de sessão/autenticação validada no servidor.
2. Não confiar em identificadores de tenant fornecidos pelo cliente.
3. Manter credenciais fora do Git e fora do navegador.
4. Testar explicitamente tentativas de acesso cruzado.
5. Automatizar migrações com controle de versão e resultado por tenant.
6. Definir backup e restauração por tenant antes da produção.

## Alternativas consideradas

- **Banco compartilhado com tenant_id:** menor custo operacional, mas exige disciplina rigorosa em todas as consultas e políticas.
- **Schema por tenant:** isolamento intermediário, porém aumenta a complexidade de migrações e administração.
- **Banco por tenant:** selecionado por corresponder ao requisito de isolamento solicitado para o produto.

## Revisão futura

Validar a compatibilidade dessa estratégia com a plataforma Corteza escolhida, seus mecanismos de autenticação, configuração e operação. Se a plataforma exigir topologia diferente, registrar nova ADR antes de alterar a decisão.
