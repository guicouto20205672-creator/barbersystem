# ADR-002 — Corteza como plataforma principal: prova de conceito obrigatória

- **Status:** decisão provisória; prova de conceito pendente.
- **Data:** 2026-11-04

## Contexto

Corteza foi escolhida inicialmente para acelerar a construção do sistema por meio de recursos low-code, APIs, automações e controle de acesso. O BarberSystem, porém, exige uma arquitetura SaaS com banco independente por empresa, experiência responsiva, regras transacionais e integrações externas.

## Evidências oficiais consultadas

- Documentação oficial: https://docs.cortezaproject.org/corteza-docs/2026.9/index.html
- Guia DevOps encontrado: https://docs.cortezaproject.org/corteza-docs/2024.9/devops-guide/index.html
- Visão da plataforma: https://cortezaproject.org/features/corteza-platform/

A documentação oficial 2026.9 descreve Corteza como plataforma low-code self-hosted, com controle de acesso e automações. A página de documentação indica Docker como caminho suportado para instalação e recomenda PostgreSQL ou MySQL em vez de SQLite em memória.

**Atenção à versão:** o guia DevOps consultado é da versão 2024.9 e identifica-se como desatualizado, indicando 2026.9 como versão estável mais recente. Portanto, exemplos de Docker Compose, versões de PostgreSQL, variáveis de ambiente e imagens do guia antigo não devem ser copiados para produção sem confirmação na documentação e nos artefatos da versão 2026.9.

## Decisão

Manter Corteza como plataforma principal candidata, condicionada à aprovação de uma prova de conceito. Não criar ainda arquivos de implantação executáveis nem fixar tags de imagem ou variáveis de ambiente com base em documentação antiga.

## Testes obrigatórios da prova de conceito

1. Subir uma instância de teste usando instruções oficiais específicas da versão escolhida.
2. Confirmar login, recuperação de acesso e ciclo de vida de usuários.
3. Modelar um módulo simples e testar CRUD pela interface e API.
4. Validar papéis, permissões e restrições no servidor.
5. Validar automações, agendamento e tratamento de falhas.
6. Testar integração de uma interface externa responsiva com as APIs.
7. Confirmar como instâncias independentes se conectam a bancos PostgreSQL separados.
8. Testar backup, restauração e atualização de versão.
9. Verificar se o modelo de operação por tenant é sustentável em custo, manutenção e monitoramento.

## Critério de aprovação

Corteza será aprovada para a arquitetura de produção somente se os testes confirmarem que a solução consegue atender o isolamento de dados por tenant e os requisitos operacionais do BarberSystem sem depender de comportamento não documentado.

Se algum requisito crítico não for atendido, registrar alternativas e impactos em uma nova ADR antes de alterar a arquitetura.

## Consequências

- Evita publicar uma configuração de infraestrutura potencialmente incompatível.
- Exige uma etapa técnica de validação antes da implementação de módulos dependentes da plataforma.
- Mantém explícito que a escolha da plataforma ainda precisa ser comprovada no cenário multiempresa do produto.
