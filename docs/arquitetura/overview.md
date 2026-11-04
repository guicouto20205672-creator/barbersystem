# Visão geral da arquitetura

**Projeto:** BarberSystem  
**Documento:** ARQ-001  
**Versão:** 1.0  
**Status:** proposta inicial — validar durante a prova de conceito.

## 1. Objetivo

Definir os limites principais do sistema antes da implementação, evitando acoplamento entre empresas, módulos e integrações externas.

## 2. Contextos do produto

- **SaaS central:** cadastro de empresas, planos, assinaturas, provisionamento, suspensão e monitoramento.
- **Ambiente da barbearia:** dashboard, agenda, fila, clientes, equipe, serviços, estoque, PDV, caixa, financeiro e relatórios.
- **Experiência do cliente:** página pública para consultar disponibilidade e realizar ou gerenciar agendamentos.
- **Integrações:** WhatsApp Business oficial e, futuramente, provedores de pagamento ou outros serviços.

## 3. Isolamento multi-tenant

A empresa (tenant) é a fronteira de propriedade dos dados. Cada empresa terá um banco de dados independente, provisionado e administrado pelo plano SaaS.

O serviço central de SaaS manterá apenas os dados necessários para identificar e administrar cada instalação, como identificador do tenant, referência segura de conexão, plano e estado da assinatura. Credenciais de banco devem permanecer em armazenamento de segredos, nunca em código ou repositório.

A resolução do tenant deve ocorrer no servidor, com autenticação e autorização verificadas em todas as operações. Não confiar em um tenant_id enviado livremente pelo navegador.

## 4. Preparação para unidades

A V1 terá uma unidade operacional por empresa, mas o modelo incluirá a entidade `units`.

- Cada tenant nasce com uma unidade principal.
- Agendamentos, vendas, caixas, estoque e movimentações operacionais referenciam uma unidade.
- Clientes permanecem no nível da empresa para permitir histórico compartilhado no futuro.
- Funcionários podem ter vínculos com unidades.
- Serviços e produtos pertencem ao tenant; disponibilidade, preço ou estoque poderão ser configurados por unidade em evolução futura.

A interface de gestão de múltiplas unidades não faz parte da V1.

## 5. Domínios e entidades principais

- Identidade: tenants, usuários, funcionários, papéis e permissões.
- Estrutura: units.
- Catálogo: services, products, categories, suppliers.
- Agenda: appointments, availability_rules, blocked_periods.
- Relacionamento: customers, customer_preferences, customer_history.
- Fila: waitlists, waitlist_entries, waitlist_offers, notification_attempts.
- Operação: sales, sale_items, payments, cash_sessions.
- Estoque: stock_movements, stock_balances, service_materials.
- Financeiro: expenses, receivables, payables, commissions.
- Integrações: messaging_channels, message_templates, integration_events.

Os nomes são conceituais e serão refinados no modelo físico após validar a plataforma e os requisitos transacionais.

## 6. Regras críticas

1. Um agendamento não pode ocupar simultaneamente o mesmo profissional e intervalo.
2. A confirmação de uma oferta da fila deve revalidar disponibilidade de forma transacional.
3. Uma oferta expirada ou recusada não pode ser aceita posteriormente.
4. A fila segue ordem de entrada entre clientes elegíveis, sem ultrapassagens.
5. Venda concluída, baixa de estoque e registro financeiro devem manter consistência.
6. Pagamento recebido não é sinônimo de faturamento; venda, recebimento, lucro e saldo de caixa são métricas distintas.
7. Toda consulta e alteração de dados operacionais deve respeitar tenant e unidade autorizados.

## 7. Plataforma

Corteza foi escolhida como plataforma principal a ser avaliada. A decisão final de implantação depende de uma prova de conceito que valide:

- versão suportada e ciclo de atualização;
- autenticação e autorização;
- modelagem e APIs;
- automações e tarefas agendadas;
- integração com serviços externos;
- estratégia de banco independente por tenant;
- backup, restauração, observabilidade e atualização.

Não publicar configurações de implantação até que esses pontos sejam verificados em documentação oficial e testados.

## 8. Ambientes

- Desenvolvimento local com dados fictícios.
- Homologação para testes integrados.
- Produção com segredos gerenciados, backups e monitoramento.

## 9. Qualidade e segurança

- Validar autorização no servidor.
- Registrar trilhas de auditoria para operações financeiras e administrativas.
- Usar transações para operações críticas.
- Aplicar validação de entrada e limites de taxa em endpoints públicos.
- Proteger dados pessoais e estabelecer política de retenção e atendimento à LGPD.
- Testar isolamento entre tenants como requisito obrigatório.
