# Agent Skills

Набор скиллов для AI-агентов: каждый скилл — это папка с `SKILL.md`, которая добавляет агенту готовые инструкции и инструменты для конкретного класса задач.

Формат `SKILL.md`, обязательные поля frontmatter, структура пакета и требования к описанию — в [спецификации Agent Skills](https://agentskills.io/specification).

## Для агентов

Инструкции по самостоятельной установке этих скиллов (куда клонировать репозиторий, как проверить результат, какие нужны зависимости) — в [AGENTS.md](AGENTS.md).

## Скиллы

### archify

Строит интерактивные HTML-диаграммы (архитектура, workflow, sequence, dataflow, lifecycle/state) из описания на естественном языке или из Mermaid. На выходе — автономный HTML с инлайн-SVG, тёмной/светлой темой, опциональной анимацией и экспортом в PNG/SVG/WebM.

Документация: [руководство](https://archify.si/guide.html) · [references/](archify/references/)

### cq

Общая база знаний для агентов. Перед задачей ищет накопленные подсказки (`query`), после находки предлагает новое знание (`propose`), подтверждает (`confirm`) или помечает устаревшее (`flag`). Работает через локальный MCP-сервер с SQLite.

Документация: [docs](https://github.com/mozilla-ai/cq/tree/main/docs)

### curl

Быстрое извлечение веб-контента: скачивает страницу через `curl` и конвертирует HTML в Markdown через `pandoc`. Подходит для документации и фактов, браузер не требуется.

Документация: [curl](https://curl.se/docs/) · [Pandoc MANUAL](https://pandoc.org/MANUAL.html)

### ddgs

Веб-поиск и получение результатов через DDGS (Dux Distributed Global Search): text, news, images, videos, books, с выводом в JSON/CSV. Запускается через `uvx`, браузер не требуется.

Документация: [DDGS](https://github.com/deedy5/ddgs)

### find-skills

Помогает найти и установить скиллы из открытой экосистемы agent skills: поиск и установка через `npx skills find/add/update`, проверка популярности и репутации источника.

Документация: [skills.sh/docs](https://skills.sh/docs) · [CLI](https://github.com/vercel-labs/skills)

### youtube-transcript

Достаёт транскрипт YouTube-видео (ручные или авто-субтитры) с таймкодами — для конспектов, цитирования и анализа содержания.

Документация: [pi-skills](https://github.com/badlogic/pi-skills)
