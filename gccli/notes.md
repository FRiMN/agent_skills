# Источник

https://github.com/badlogic/pi-skills/blob/main/gccli/

# Changelog

## 2026-11-16 — правки SKILL.md по итогам проверки на практике

- **Setup**: добавлено примечание про OAuth consent screen (user type External + publishing status Testing) — refresh token живёт 7 дней; при ошибке `invalid_grant` нужен повторный `gccli accounts add <email>` либо перевод приложения в In production.
- **Date/Time Format**: исправлено неверное утверждение про локальное время. Время без зоны (`YYYY-MM-DDTHH:MM:SS`) Google отклоняет с `Error: Missing time zone definition for start time.` — нужен UTC (`...Z`) или явное смещение (`...+07:00`). Добавлено, что вывод `events` / `event` показывается в локальной зоне.
- **Behavior Notes** (новый раздел):
  - `delete` — soft-delete: печатает `Deleted`, событие исчезает из `events`, но `event <id>` всё ещё отдаёт запись со `Status: cancelled`.
  - редкие подвисания вызовов без вывода → повторить запрос или обернуть в `timeout 30`.
