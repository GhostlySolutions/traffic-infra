# Traffic Infra

Infrastructure configuration for the **Ghostly Solutions Traffic Platform**.

---

## Overview

This repository contains environment and infrastructure configuration for the Traffic stack, which powers Ghostly Solutions services.

| Component | Description | Host |
|------------|--------------|------|
|  PostgreSQL 16 | Primary transactional database (`traffic`) | `cp-01` |
|  Redis | Cache and message queues | `cp-01` |
|  ClickHouse | Analytical storage (`traffic_api`) | `ch-01 (162.243.22.121)` |
|  API | Express + TypeScript service | `cp-01:3001` |

---

##  Environment (.env.staging)

Stored securely at `/root/secrets/traffic.env.staging` on the server.


Как запустить API/EDGE локально с .env.staging

Скопировать staging-конфигурацию:

cp /root/secrets/traffic.env.staging .env


Запустить все сервисы:

docker compose -f docker-compose.prod.yml up -d --build


Проверить, что API запущен:

curl http://localhost:3001/healthz


Ожидаемый ответ:

{ "status": "ok" }


(Опционально) Проверить доступ к Redis и ClickHouse:

redis-cli -h cp-01 ping

curl -s "http://default:clickpass@162.243.22.121:8123/ping"
