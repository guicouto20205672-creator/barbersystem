# Agenda — BS-UI-002

**Versão:** 1.0  
**Status:** especificação inicial para revisão antes da implementação.

## 1. Objetivo

Permitir que a barbearia organize a disponibilidade dos profissionais e que clientes agendem serviços pela web, sem oferecer horários ocupados ou permitir reservas duplicadas.

## 2. Experiências

### Área administrativa
- Visualização da agenda geral e por profissional.
- Navegação por dia e semana.
- Filtros por profissional e estado do agendamento.
- Abertura de detalhes do atendimento.
- Criação de agendamento pela recepção.
- Cancelamento e remarcação conforme permissões.
- Bloqueio de períodos e consulta ao histórico.

### Página do cliente
- Escolher serviço.
- Escolher profissional ou opção de qualquer profissional, se habilitada.
- Escolher data.
- Consultar horários realmente disponíveis.
- Confirmar agendamento.
- Consultar os próprios agendamentos.
- Cancelar ou solicitar remarcação conforme política da empresa.

## 3. Dados necessários

Um agendamento deve registrar, no mínimo:
- tenant;
- unidade;
- cliente;
- serviço;
- profissional;
- início e fim;
- estado;
- origem (cliente, recepção ou outro canal autorizado);
- observações permitidas;
- datas de criação e atualização.

O preço e a duração aplicados devem ser preservados como fotografia do momento da reserva, para que mudanças futuras no cadastro do serviço não alterem atendimentos já marcados.

## 4. Estados sugeridos

- Pendente de confirmação, quando a política da empresa exigir.
- Confirmado.
- Em atendimento.
- Concluído.
- Cancelado.
- Não compareceu.

A transição entre estados deve ser validada no servidor e registrada para auditoria. Estados e transições finais serão confirmados na implementação.

## 5. Cálculo de disponibilidade

Um horário só pode ser apresentado se:
1. O serviço estiver ativo e disponível para o profissional/unidade.
2. O profissional estiver habilitado para o serviço.
3. O horário estiver dentro do expediente e da disponibilidade configurada.
4. Não houver bloqueio aplicável.
5. Não houver outro agendamento que se sobreponha ao intervalo.
6. A unidade estiver habilitada para operar.

A duração do serviço deve ser considerada no intervalo completo, não apenas no horário inicial. Regras de intervalo entre atendimentos (buffer) devem ser configuráveis se aprovadas no detalhamento.

## 6. Prevenção de conflito

A verificação na interface é apenas informativa. No momento de gravar, o servidor deve revalidar a disponibilidade e aplicar uma proteção transacional contra reservas concorrentes.

Duas solicitações simultâneas para o mesmo profissional e intervalo não podem resultar em duas reservas confirmadas.

A validação também deve considerar alterações de horário, profissional, serviço e cancelamentos.

## 7. Regras de cancelamento e remarcação

- Aplicar a política de antecedência configurada pela empresa.
- Atualizar o estado do agendamento no servidor.
- Registrar autor, horário e motivo quando fornecido.
- Ao liberar um horário, disparar o processo da fila inteligente quando houver clientes elegíveis.
- A fila deve competir pela vaga com revalidação transacional; não reservar apenas com base em uma notificação enviada.

Os limites de antecedência e a política de cancelamento são configurações pendentes de decisão comercial.

## 8. Permissões

- Proprietário e gerente: acesso conforme permissões administrativas.
- Recepção: criar e gerenciar agendamentos conforme permissões.
- Barbeiro: consultar a própria agenda e atualizar estados permitidos.
- Cliente: consultar e alterar somente os próprios agendamentos, dentro da política.

Todas as regras devem ser aplicadas no servidor.

## 9. Notificações

Eventos candidatos a notificação:
- agendamento criado;
- confirmação;
- lembrete;
- cancelamento;
- alteração de data ou horário;
- oferta de horário pela fila.

A integração WhatsApp será especificada separadamente e deve respeitar consentimento, templates e políticas oficiais.

## 10. Responsividade e acessibilidade

- Desktop: calendário com visualização geral e filtros laterais.
- Celular: lista cronológica e seleção de data com controles adequados ao toque.
- Estados visuais distintos e legíveis.
- Não depender apenas de cor para comunicar o estado.
- Exibir fuso horário da unidade e evitar ambiguidade em horários.

## 11. Critérios de aceite

- O cliente só visualiza horários válidos para o serviço e profissional escolhidos.
- Horários ocupados ou bloqueados não são oferecidos.
- Tentativas simultâneas não criam duplicidade.
- Duração do serviço é respeitada no intervalo.
- Cancelamentos e remarcações atualizam a agenda.
- A liberação de horário pode acionar a fila inteligente.
- Cada usuário acessa apenas dados permitidos do tenant e unidade.
- A agenda pode ser utilizada em desktop e celular.

## 12. Decisões pendentes

- Expediente padrão e exceções por profissional.
- Antecedência mínima e máxima para agendar.
- Política de cancelamento e remarcação.
- Duração padrão e possibilidade de duração específica por profissional.
- Intervalo (buffer) entre atendimentos.
- Se agendamentos do cliente ficam confirmados imediatamente ou dependem de aprovação.
- Política para atrasos e não comparecimento.
