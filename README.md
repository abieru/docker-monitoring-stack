# Stack de Monitoramento

Stack completa para monitoramento do sistema e containers Docker, similar ao TrueNAS Scale.

## Serviços

| Serviço | Porta | Função |
|---------|-------|--------|
| **Prometheus** | 9090 | Banco de dados de métricas |
| **Grafana** | 3000 | Dashboards visuais |
| **Node Exporter** | 9100 | Métricas do sistema (CPU, memória, disco, rede) |
| **cAdvisor** | 18080 | Métricas dos containers Docker |
| **Homarr** | 7575 | Dashboard inicial (clima, status, apps, Docker) |

## Como usar

1. Suba os serviços:
```bash
cd monitoring
docker compose up -d
```

2. Acesse os serviços:
- **Homarr** (dashboard inicial): http://localhost:7575
- **Grafana**: http://localhost:3000 (usuário: `admin`, senha: `admin`)
- **Prometheus**: http://localhost:9090

3. Configure o Homarr pela primeira vez:
- Abra http://localhost:7575 e clique em **"Edit"** no canto superior direito
- Adicione widgets como:
  - **Clock** — relógio
  - **Weather** — clima da sua cidade
  - **Docker** — containers Docker ativos
  - **Ping / Status** — status dos seus serviços (Prometheus, Grafana, Plex, etc.)
  - **Bookmarks / Apps** — atalhos para todos os seus apps

4. Os dashboards do Grafana já vêm provisionados automaticamente. Acesse-os em:
- **Dashboards > Browse** no Grafana
- **Node Exporter Full** — métricas completas do sistema
- **Node Exporter Disk** — focado em armazenamento/disco
- **Docker Monitoring** — containers Docker ativos

## O que você vai ver

- **Homarr**: Dashboard inicial bonito com clima, relógio, atalhos para apps e status dos serviços
- **Grafana**: Uso de CPU, memória RAM, memória swap e disco
- **Grafana**: Temperatura (se suportado pelo hardware)
- **Grafana**: Rede (upload/download)
- **Grafana**: Todos os containers Docker ativos, uso de recursos por container
- **Grafana**: Status de saúde dos serviços

## Dicas

- A senha padrão do Grafana é `admin`/`admin`. Mude após o primeiro login.
- Os dados ficam persistidos nos volumes Docker (`prometheus_data`, `grafana_data`, `homarr_data`).
- O **Homarr** salva sua configuração em `/app/data` — não apague o volume `homarr_data`.
- Para adicionar ao seu `media-server` existente, basta copiar os serviços do `docker-compose.yml` para o seu arquivo principal e ajustar a rede.
