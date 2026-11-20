# Протокол функциональных испытаний (19.11.2026)

Стенд: CTRL-01 192.168.20.10, MON-01 192.168.20.11, DB-01 192.168.20.12, IOT-01 192.168.30.10.

| № | Проверка | Исходные данные | Ожидаемый результат | Фактический результат | Подтверждение |
|---|----------|-----------------|---------------------|-----------------------|---------------|
| 1 | Поступление TEMP-01 и HUM-01 | поток Node-RED активен | новые показания каждые 5 с | интервал 5 с, в БД 31 333 записи | screens/w8_history.png |
| 2 | Вентилятор при температуре выше порога | TEMP = 31 | FAN-01 ON | state=ON, режим auto | actuator_events, id 10594–10598 |
| 3 | Вентилятор ниже порога | TEMP = 25 | FAN-01 OFF | state=OFF | actuator_events, id 10591–10593 |
| 4 | Вентилятор на границе | TEMP = 30 | FAN-01 OFF | state=OFF | actuator_events, id 10591–10593 |
| 5 | Запись в SQLite | сообщения от Node-RED | новые строки в двух таблицах | measurements и actuator_events пополняются | screens/w8_history.png |
| 6 | История в веб-интерфейсе | открыт http://192.168.20.12:8081 | карточки, график, таблица | 31 333 записи, карточки и история отображаются | screens/w8_history.png |
| 7 | Цель Prometheus | job office-controller | UP | UP | screens/w8_prometheus_target.png |
| 8 | Оповещение TEMP-01 | остановлена отправка TEMP | Alerting | firing, возраст 48 с | screens/w8_alert_temp.png |
| 9 | Отличие от пропажи CTRL | приёмник остановлен | правило CTRL firing, датчики — inactive | up=0, CTRL firing | screens/w8_alert_ctrl.png |
| 10 | Доставка письма | SMTP Яндекса | письмо в ящике | получены [FIRING] 17:54 и [RESOLVED] 17:55 | screens/mail-evidence.txt |
