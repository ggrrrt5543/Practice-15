# Снимок состояния стенда (19.11.2026)

- CTRL-01: приёмник v3, `:8080`, `/health` — ok, `/metrics` отдаёт данные.
- IOT-01: Node-RED `:1880`, поток «Умный офис: датчики и вентилятор» активен,
  отправка TEMP/HUM каждые 5 с на CTRL и DB.
- DB-01: сервис хранения `:8081`, SQLite `telemetry.sqlite3`, 31 333 записи,
  страница истории работает.
- MON-01: Prometheus — цель `office-controller` UP; Grafana — панель
  `office-controller-lab`, три правила в группе `office-sensors` (TEMP-01, HUM-01, CTRL-01),
  состояние Normal.
- Оповещения: при остановке TEMP-01 правило TEMP-01 → Alerting; при остановке приёмника
  правило CTRL-01 → Alerting, правила датчиков — inactive.
- SMTP: настроен на `kutuzowya@yandex.ru`, письма доставляются: получены
  [FIRING] TEMP-01 (17:54) и [RESOLVED] TEMP-01 (17:55) — см. screens/mail-evidence.txt.
