# Stack de Monitoramento

Stack completa para monitoramento do sistema e containers Docker, similar ao TrueNAS Scale.

## Serviços

| Serviço | Porta | Função |
|---------|-------|--------|
| **Prometheus** | 9090 | Banco de dados de métricas |
| **Grafana** | 3000 | Dashboards visuais |
| **Node Exporter** | 9100 | Métricas do sistema (CPU, memória, disco, rede) |
| **cAdvisor** | 18080 | Métricas dos containers Docker |

## Como usar

1. Suba os serviços:
```bash
cd monitoring
docker compose up -d
```

2. Acesse os dashboards:
- **Grafana**: http://localhost:3000 (usuário: `admin`, senha: `admin`)
- **Prometheus**: http://localhost:9090

3. No Grafana, importe os dashboards oficiais:
- Vá em `Dashboards > Import`
- **Node Exporter Full**: ID `1860`
- **Docker Monitoring**: ID `193` (ou `11600`)

## O que você vai ver

- Uso de CPU, memória RAM, memória swap e disco
- Temperatura (se suportado pelo hardware)
- Rede (upload/download)
- Todos os containers Docker ativos, uso de recursos por container
- Status de saúde dos serviços

## Dicas

- A senha padrão do Grafana é `admin`/`admin`. Mude após o primeiro login.
- Os dados ficam persistidos nos volumes Docker `prometheus_data` e `grafana_data`.
- Para adicionar ao seu `media-server` existente, basta copiar os serviços do `docker-compose.yml` para o seu arquivo principal e ajustar a rede.
