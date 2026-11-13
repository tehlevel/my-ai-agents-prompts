# AI Architect v7.0 (Draft — Gemini 4 Native Edition)

## Описание
Мета-агент для проектирования системных инструкций, мульти-агентных топологий и конфигурационной документации под экосистему моделей Google Gemini 4 (`Carbon`, `Argon`, `Hydrogen`, `Decisions API`, `3.5 Flash-Lite`). Работает как консультант с учетом целевой среды запуска.

## Ключевые особенности
- **Gemini 4 Parameter Matrix:** Полный отказ от устаревших `temperature`/`top_p`/`top_k` и `thinking_budget` в пользу связки `Model Tier` + `thinking_level` (`low`/`medium`/`high`/`xhigh`) + `Structured Outputs`.
- **Alignment Check:** Прозрачная диагностическая шапка без конфликтующего с нативным Reasoning тега `<thinking>`.
- **Adaptive Multi-Agency:** Автоматическая оценка уместности одиночного агента или связки *Orchestrator / Worker / Verifier / Router*.
- **Environment-Aware & Cache-Friendly:** Подстройка опций под среду запуска (AI Studio, API/SDK, Agentic IDE) и порядок секций `Static-First` для автоматического Implicit Caching (≥ 4,096 токенов).
- **Multilingual Grounding:** Осознанный выбор языкового режима (Гибридный / Моноязычный / English-Core) с явной фиксацией языка вывода.

## Рекомендуемые параметры (Configuration)
*Основано на архетипе: Type 1 — Deep Architecture & Prompt Engineering*
*Целевая среда: Google AI Studio / Gemini API (Interactive Consultation)*

| Параметр | Значение | Обоснование |
| :--- | :--- | :--- |
| **Model Tier** | `gemini-4-argon` (или `gemini-4-hydrogen` на `xhigh`) | Баланс глубокой архитектурной логики и скорости итераций; для самых сложных мульти-агентных систем — `gemini-4-carbon`. |
| **Thinking Level** | `medium` / `high` (для Carbon/Argon) или `high` (для Hydrogen) | Обеспечивает самопроверку противоречий в спецификациях и корректный подбор топологии. |
| **Max Output Tokens** | `32,768` – `65,536` | Запас обязателен, чтобы токены нативного Reasoning не обрезали финальные артефакты кода. |
| **Sampling (`temp`/`top_p`)** | Не задавать (удалить) | Игнорируются в Gemini 4 и вызывают deprecation-предупреждения / будущие HTTP 400. |
| **Tools & Capabilities** | `Google Search` (ON опционально), `Structured Outputs` (OFF) | Поиск полезен при проверке актуальных API-спецификаций сторонних сервисов; основной вывод — Markdown. |

## Структура
Path: `/01-AI-Builders/AI-Architect-v7-Draft/`
- `README.md`
- `SYSTEM_PROMPT.md`