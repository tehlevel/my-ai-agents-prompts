# AI Architect v7.1 (Gemini 4 Native Edition)

## Описание
Агент-архитектор для проектирования системных инструкций, мульти-агентных топологий и конфигурационной документации под экосистему моделей Google Gemini 4 (`Carbon`, `Argon`, `Hydrogen`, `Decisions API`, `3.5 Flash-Lite`). Работает как эксперт-консультант с адаптацией под целевую среду запуска и сложность задачи.

## Ключевые особенности
- **Gemini 4 Parameter Matrix:** Актуальная конфигурация без устаревших `temperature`/`top_p`/`top_k`, `frequency_penalty`/`presence_penalty` и `thinking_budget`; управление через `Model Tier` + `thinking_level` (`low`/`medium`/`high`/`xhigh`) + `Structured Outputs` + нативный `Function Calling`.
- **Proportional Design:** Легковесные промпты для простых персональных агентов и расширенные спецификации (усиленный `Security`, `Handoff Protocol`, `Static-First`) для продакшн- и мульти-агентных систем.
- **Adaptive Multi-Agency:** Проектирование как одиночных агентов, так и связок *Orchestrator / Worker / Verifier / Router* с четким контрактом передачи данных.
- **Hardened Input & Search Isolation:** Изоляция вставленных черновиков промптов и результатов `Google Search` от Indirect Prompt Injection, плюс конфиденциальность собственных инструкций.
- **Environment-Aware & Alignment Check:** Внедрение только релевантных среде опций и прозрачный однострочный статус фокуса вместо тега `<thinking>`.

## Рекомендуемые параметры (Configuration)
*Основано на архетипе: Type 1 — Deep Architecture & Prompt Engineering*
*Целевая среда: Google AI Studio / Gemini API (Interactive Consultation)*

| Параметр | Значение | Обоснование |
| :--- | :--- | :--- |
| **Model Tier** | `gemini-4-argon` (или `gemini-4-hydrogen` на `xhigh`) | Оптимальный баланс глубины архитектурного анализа и скорости итераций; для сложных мульти-агентных систем — `gemini-4-carbon`. |
| **Thinking Level** | `medium` / `high` (для Carbon/Argon) или `high` / `xhigh` (для Hydrogen) | Обеспечивает проверку логических противоречий, корректный подбор топологии и валидацию шаблонов. |
| **Max Output Tokens** | `32,768` – `65,536` | Достаточный буфер, чтобы токены нативного мышления не обрезали генерацию финальных артефактов. |
| **Sampling & Penalties** | Не задавать (удалить) | `temperature`, `top_p`, `top_k`, `frequency_penalty`, `presence_penalty` в Gemini 4 не поддерживаются. |
| **Tools & Capabilities** | `Google Search` (опционально), `Structured Outputs` (OFF) | Поиск полезен при проверке свежих спецификаций сторонних API/SDK; основной вывод — Markdown. |

## Структура
Path: `/01-AI-Builders/AI-Architect/`
- `README.md`
- `SYSTEM_PROMPT.md`
- `_archive/` *(предыдущие версии)*