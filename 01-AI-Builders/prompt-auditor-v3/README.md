# Prompt-Auditor v2.0 (Gemini 4 & Architect v7.0 Companion)

## Описание
Независимый сеньор-ревьюер и Red-Team аудитор системных промптов, конфигурационных `README.md` и мульти-агентных сборок. Работает в чистом контексте без привязки к истории разработки: проверяет безопасность (Direct & Indirect Prompt Injection), совместимость с Gemini 4, экономику кэша/токенов, логику стыков между агентами и выдает точечные Diff-правки.

## Конфигурация среды
- **Режим:** Single-Agent (Adversarial Reviewer & Gemini 4 Linter)
- **Целевая среда:** Google AI Studio / Chat UI
- **Языковой стандарт:** Гибридный (структура EN, разбор RU, сохранение языка проверяемого кода в Diff)

## Ключевые особенности
- **Гибкий ввод в чате:** Принимает как связку `README.md` + `SYSTEM_PROMPT*.md` из `AI Architect v7.0`, так и сырой текст промпта с описанием задачи (или `<intent>`/`<draft_prompt>`).
- **Gemini 4 Linter:** Вылавливает устаревшие параметры (`temperature`, `top_p`, `thinking_budget`, `MINIMAL`), псевдо-`<thinking>` теги, микро-менеджмент рассуждений и ошибки `Static-First` кэширования.
- **Proportional Review:** Не навязывает избыточные схемы (JSON, тяжелый Security) простым бытовым ботам; усиливает строгость для туловых, API- и мульти-агентных систем.
- **Stress-Test Simulation:** Прогоняет 2–3 реалистичных сценария поломки (IPI через файлы/URL, сбой инструмента, зацикливание Handoff) прямо в отчете.

## Рекомендуемые параметры (Configuration)
*Основано на архетипе: Type 1 — Deep Architecture, Security & Hard Logic*
*Целевая среда: Google AI Studio / Chat UI*

| Компонент / Роль | Model Tier | Thinking Level | Инструменты и опции среды | Обоснование |
| :--- | :--- | :--- | :--- | :--- |
| **Prompt-Auditor v2.0** | `gemini-4-carbon` *(или `gemini-4-argon` / `gemini-4-hydrogen`)* | `medium` / `high` *(для Hydrogen: `high` / `xhigh`)* | `Google Search`: OFF, `URL Context`: OFF, `Structured Outputs`: OFF | `Carbon` (или `Hydrogen xhigh`) обеспечивает максимальную глубину Red-Team симуляции и поиск скрытых логических тупиков без «поддакивания». |

*(Примечание: для сохранения независимости аудита запускайте каждую крупную проверку в новом чистом чате).*

## Структура
Path: `/01-AI-Builders/Prompt-Auditor/`
- `README.md`
- `SYSTEM_PROMPT.md`
- `_archive/` *(архивная версия для Gemini 3)*