# Dashboard — BS-UI-001

**Versão:** 1.0  
**Status:** especificação funcional concluída; implementação e testes pendentes.

## 1. Objetivo

Apresentar ao proprietário uma visão rápida e confiável da situação financeira e operacional da barbearia após o login.

## 2. Estrutura da tela

### Desktop
- Sidebar lateral fixa e recolhível.
- Cabeçalho com nome da barbearia, período selecionado, notificações e perfil.
- Área principal em cartões, gráficos, agenda resumida e alertas.

### Celular
- Navegação compacta e adaptada ao toque.
- Conteúdo em coluna, sem exigir rolagem horizontal.
- Filtros e ações acessíveis em telas menores.

## 3. Navegação principal

1. Visão geral
2. Agenda
3. Fila inteligente
4. Clientes
5. Funcionários
6. Serviços
7. Estoque
8. PDV
9. Caixa
10. Financeiro
11. Relatórios
12. Configurações

## 4. Filtros

Períodos disponíveis:
- Hoje
- Ontem
- Últimos 7 dias
- Últimos 30 dias
- Mês atual
- Mês anterior
- Personalizado

Todos os indicadores e gráficos devem respeitar o período, tenant e unidade autorizada.

## 5. Indicadores financeiros

- Faturamento.
- Despesas.
- Lucro gerencial estimado.
- Saldo disponível.

### Definições obrigatórias

- **Faturamento:** vendas finalizadas, descontados descontos e estornos, conforme regra contábil/gerencial definida.
- **Recebimentos:** valores efetivamente recebidos; apresentar separadamente das vendas.
- **Lucro estimado:** indicador gerencial após custos e despesas conhecidos, claramente identificado como estimativa.
- **Saldo disponível:** posição real do caixa/contas consideradas no sistema.
- Venda parcialmente recebida não pode ser apresentada como dinheiro integralmente disponível.

## 6. Indicadores operacionais

- Agendamentos.
- Atendimentos concluídos.
- Cancelamentos.
- Atendimentos em andamento.
- Barbeiros ativos no período.
- Clientes novos.

## 7. Gráficos

- Evolução financeira no período.
- Desempenho dos barbeiros.
- Serviços mais vendidos.

Os gráficos devem indicar unidade de medida, período e ausência de dados quando aplicável.

## 8. Agenda resumida

Mostrar os próximos atendimentos do dia com horário, cliente, serviço, profissional e estado, respeitando as permissões do usuário.

## 9. Alertas

- Estoque abaixo do mínimo.
- Próximos agendamentos e conflitos.
- Ofertas pendentes ou falhas da fila.
- Caixa aberto ou divergências.
- Contas vencidas ou próximas do vencimento.
- Falhas na integração WhatsApp.

## 10. Permissões

- Proprietário: visão completa da empresa.
- Gerente: indicadores e ações concedidas.
- Recepção: dados operacionais necessários ao atendimento.
- Barbeiro: agenda e indicadores próprios autorizados.

Ocultar componentes na interface não substitui autorização no servidor.

## 11. Estados da interface

- Carregamento.
- Erro com possibilidade de tentar novamente.
- Estado vazio com orientação para cadastrar dados.
- Dados disponíveis.
- Período sem movimento.

Valores ilustrativos em protótipos devem ser identificados como demonstração, nunca confundidos com dados reais.
