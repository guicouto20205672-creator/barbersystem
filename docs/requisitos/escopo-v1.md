# Escopo funcional — versão 1

**Documento:** RF-001  
**Versão:** 1.0  
**Status:** baseline inicial para detalhamento e validação.

## 1. Perfis e ambientes

- **Proprietário:** acesso administrativo e visão completa da empresa.
- **Gerente:** operação e gestão conforme permissões concedidas.
- **Recepção:** agenda, clientes, vendas e caixa conforme permissões.
- **Barbeiro:** própria agenda, atendimentos e informações autorizadas.
- **Cliente:** página pública para agendamento e gerenciamento dos próprios dados.
- **Administrador SaaS:** provisionamento e administração das contas empresariais.

A autorização deve ser validada no servidor em cada operação.

## 2. Módulos da V1

### Dashboard
- Indicadores financeiros e operacionais por período.
- Faturamento, despesas, lucro gerencial estimado e saldo disponível.
- Agendamentos, cancelamentos, atendimentos e clientes novos.
- Desempenho de barbeiros e serviços.
- Alertas de estoque, agenda, fila, caixa e integrações.

### Agenda
- Cliente escolhe serviço, profissional, data e horário.
- Exibir apenas horários disponíveis.
- Criar, cancelar e remarcar agendamentos.
- Agenda geral e individual, histórico e estados.
- Bloqueios de horário e prevenção de reservas duplicadas.

### Fila de espera inteligente
- Cliente registra preferências de dias, horários e profissional.
- Ao liberar horário, localizar clientes elegíveis.
- Notificar um cliente por vez, em ordem de entrada.
- Conceder 5 minutos para aceitar.
- Se recusar ou expirar, avançar ao próximo elegível.
- Respostas fora do prazo não confirmam o horário.
- Revalidar disponibilidade no momento da aceitação.
- Registrar ofertas, respostas, expirações e falhas de notificação.
- Se ninguém aceitar, disponibilizar o horário normalmente.

### Clientes (CRM)
- Cadastro e dados de contato.
- Histórico de agendamentos, serviços e compras.
- Preferências de profissional e serviço.
- Última visita e identificação de clientes inativos.
- Ações de relacionamento com consentimento e controles aplicáveis.

### Funcionários
- Cadastro e login individual.
- Perfis e permissões.
- Agenda, atendimentos, comissões e desempenho.
- Acesso limitado conforme função.

### Serviços
- Cadastro, duração, preço e estado ativo/inativo.
- Associação a profissionais habilitados.

### Estoque
- Produtos, categorias e fornecedores.
- Quantidade, custo, preço e estoque mínimo.
- Entradas, saídas, perdas e ajustes.
- Alertas de reposição.
- Baixa integrada a vendas e consumo de materiais por serviço, quando configurado.

### PDV e caixa
- Venda de serviços e produtos.
- Descontos autorizados e meios de pagamento.
- Histórico e comprovante.
- Abertura e fechamento de caixa.
- Registro de pagamentos parciais quando aplicável.
- Integração consistente com estoque e financeiro.

### Financeiro e relatórios
- Receitas, recebimentos, despesas e contas.
- Fluxo de caixa e fechamentos por período.
- Faturamento por serviço e profissional.
- Despesas fixas e variáveis.
- Lucro gerencial estimado e relatórios.
- Separar venda realizada, valor recebido, lucro e saldo disponível.

### WhatsApp
- Canal configurado por empresa (tenant).
- Confirmações, lembretes, cancelamentos e ofertas da fila.
- Registro de status e tentativas.
- Utilizar integração oficial e respeitar templates, consentimento e políticas do provedor.

### Administração SaaS
- Cadastro e provisionamento de tenants.
- Plano, assinatura e estado da conta.
- Suspensão e reativação.
- Monitoramento operacional.
- Banco de dados independente por tenant.

## 3. Requisitos multiempresa e unidades

- RF-015: cada empresa terá ao menos uma unidade.
- RF-016: a V1 permitirá uma unidade operacional por empresa.
- RF-017: todo agendamento identifica sua unidade.
- RF-018: estoque e movimentações identificam unidade.
- RF-019: vendas e sessões de caixa identificam unidade.
- RF-020: clientes pertencem à empresa.
- RF-021: funcionários podem ter vínculos com unidades.
- RF-022: a arquitetura deve permitir múltiplas unidades no futuro, sem habilitar sua gestão na V1.

## 4. Requisitos não funcionais

- Interface responsiva para computador e celular.
- Identidade visual premium em preto, dourado e cinza, com branco de apoio.
- Isolamento de dados entre tenants.
- Segurança de autenticação, autorização e segredos.
- Auditoria de ações críticas.
- Consistência transacional para agenda, fila, vendas, estoque e pagamentos.
- Backups e procedimento de restauração testados.
- Tratamento de estados de carregamento, erro e ausência de dados.

## 5. Fora do escopo inicial

- Gestão operacional de várias unidades na interface.
- Aplicativos nativos publicados em lojas.
- Integrações de pagamento não validadas.
- Recursos avançados de marketing automatizado sem definição de consentimento e política.

## 6. Critérios gerais de aceite

- Um tenant não consegue consultar ou alterar dados de outro.
- Horários ocupados não podem ser reservados em duplicidade.
- A fila oferece vagas em ordem e respeita o prazo de 5 minutos.
- Uma oferta expirada não pode ser aceita.
- Venda concluída atualiza os registros de estoque, pagamento e caixa corretamente.
- Usuários só acessam as funções autorizadas.
- A experiência funciona em telas de celular e desktop.
