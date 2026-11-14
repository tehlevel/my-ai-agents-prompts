# AI Architect v7.0 (Gemini 4 Native Edition)

## Описание
Агент-архитектор для проектирования системных инструкций, мульти-агентных топологий и конфигурационной документации под экосистему моделей Google Gemini 4 (`Carbon`, `Argon`, `Hydrogen`, `Decisions API`, `3.5 Flash-Lite`). Работает как эксперт-консультант с адаптацией под целевую среду запуска и сложность задачи.

## Ключевые особенности
- **Gemini 4 Parameter Matrix:** Актуальная конфигурация без устаревших `temperature`/`top_p`/`top_k` и `thinking_budget`; управление через `Model Tier` + `thinking_level` (`low`/`medium`/`high`/`xhigh`) + `Structured Outputs`.
- **Proportional Design:** Легковесные промпты для простых персональных агентов и расширенные спецификации (расширенный `Security`, `Handoff Protocol`, `Static-First`) для продакшн- и мульти-агентных систем.
- **Adaptive Multi-Agency:** Проектирование как одиночных агентов, так и связок *Orchestrator / Worker / Verifier / Router* с четким контрактом передачи данных.
- **Environment-Aware:** Внедрение только тех опций (`Long Decode`, `Agentic Video`, `Structured Outputs`, HTTP-таймауты, `thought_signature`), которые доступны в целевой среде.
- **Alignment Check:** Прозрачный однострочный статус фокуса вместо конфликтующего с нативным Reasoning тега `<thinking>`.

## Рекомендуемые параметры (Configuration)
*Основано на архетипе: Type 1 — Deep Architecture & Prompt Engineering*
*Целевая среда: Google AI Studio / Gemini API (Interactive Consultation)*

| Параметр | Значение | Обоснование |
| :--- | :--- | :--- |
| **Model Tier** | `gemini-4-argon` (или `gemini-4-hydrogen` на `xhigh`) | Оптимальный баланс глубины архитектурного анализа и скорости итераций; для сложных мульти-агентных систем — `gemini-4-carbon`. |
| **Thinking Level** | `medium` / `high` (для Carbon/Argon) или `high` (для Hydrogen) | Обеспечивает проверку логических противоречий, корректный подбор топологии и валидацию шаблонов. |
| **Max Output Tokens** | `32,768` – `65,536` | Достаточный буфер, чтобы токены нативного мышления не обрезали генерацию длинных артефактов. |
| **Sampling (`temp`/`top_p`)** | Не задавать (удалить) | Игнорируются в Gemini 4 и вызывают deprecation-предупреждения / будущие HTTP 400. |
| **Tools & Capabilities** | `Google Search` (опционально), `Structured Outputs` (OFF) | Поиск полезен только при проверке свежих спецификаций внешних API; основной вывод — Markdown. |

## Структура
Path: `/01-AI-Builders/AI-Architect/`
- `README.md`
- `SYSTEM_PROMPT.md`
- `_archive/` *(предыдущие версии, включая v6.5)*