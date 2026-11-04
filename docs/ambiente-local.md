# Ambiente local — prova de conceito Corteza

**Objetivo:** executar uma instalação de desenvolvimento do BarberSystem com uma instância Corteza e um PostgreSQL. Este ambiente é apenas para validação local; não é a arquitetura de produção multi-tenant.

## Requisitos

- Computador com Docker Desktop instalado e em execução.
- Docker Compose v2 disponível pelo comando `docker compose`.
- Git (opcional, para clonar o repositório).

A configuração foi baseada no exemplo oficial de Docker Compose da documentação Corteza 2026.9. A imagem está fixada em `2026.9.0`, evitando atualização inesperada pelo uso de `latest`.

## Arquivos

- `docker-compose.yml`: serviços Corteza, PostgreSQL e Corredor.
- `.env.example`: modelo sem credenciais reais.
- `.env`: arquivo local criado por você; fica fora do Git.

## Preparação

1. Clone o repositório no computador.
2. Na pasta `barbersystem`, copie `.env.example` para um novo arquivo chamado `.env`.
3. Edite `.env` e troque os valores de exemplo:
   - `POSTGRES_PASSWORD`: senha local forte.
   - `DB_DSN`: atualize a senha dentro da URL para ser exatamente igual à senha acima.
   - `AUTH_JWT_SECRET`: use um valor aleatório longo e exclusivo.
4. Não envie o arquivo `.env` para o GitHub e não compartilhe capturas que revelem os valores.

## Inicialização

No terminal, dentro da pasta do projeto:

```bash
docker compose pull
docker compose up -d
docker compose ps
```

Quando os serviços estiverem em execução, abra:

`http://localhost:18091`

A primeira inicialização pode levar alguns minutos. Consulte os logs se o serviço ainda não estiver pronto:

```bash
docker compose logs -f server
```

Para interromper os serviços sem apagar o banco:

```bash
docker compose down
```

**Não use** `docker compose down -v` se quiser preservar o banco local: a opção `-v` remove volumes.

## O que esta prova de conceito valida

- Inicialização da Corteza 2026.9.0.
- Conexão com PostgreSQL 15.
- Disponibilidade das aplicações web da Corteza.
- Inicialização do serviço Corredor para automações.
- Persistência dos dados após reiniciar os contêineres.

## O que ainda não valida

- Provisionamento automático de tenants.
- Banco independente por empresa.
- Segurança completa do SaaS e isolamento entre clientes.
- Domínio público, HTTPS, e-mail, WhatsApp ou pagamentos.
- Backups externos, restauração testada, monitoramento e alta disponibilidade.

Não exponha a porta local na internet. O mapeamento está limitado a `127.0.0.1` para que o ambiente de teste fique acessível apenas no próprio computador.

## Observações técnicas

- A documentação oficial de atualização recomenda fixar a versão da imagem e definir `AUTH_JWT_SECRET` para evitar invalidação inesperada das sessões após recriação do contêiner.
- O exemplo oficial local usa Corteza, PostgreSQL e Corredor.
- A configuração `platform: linux/amd64` segue o exemplo oficial. Em máquinas ARM, a compatibilidade e o desempenho precisam ser avaliados.
- Use apenas dados fictícios neste ambiente.
