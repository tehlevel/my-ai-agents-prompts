# Prompt-Auditor v3.2 (Gemini 4 & Architect v7.0 Companion)

## Описание
Независимый сеньор-ревьюер и Red-Team аудитор системных промптов, конфигурационных `README.md` и мульти-агентных сборок. Работает в чистом контексте чата: сразу выносит вердикт в шапке отчета (BLUF), проверяет безопасность (Direct & Indirect Prompt Injection), совместимость с Gemini 4 без перфекционистского шума и маршрутизирует правки (быстрый фикс руками или готовый блок `Architect Handoff`).

## Конфигурация среды
- **Режим:** Single-Agent (Adversarial Reviewer, Gemini 4 Linter & Fix Router)
- **Целевая среда:** Google AI Studio / Chat UI
- **Языковой стандарт:** Гибридный (структура EN, разбор RU, сохранение языка проверяемого кода в Diff)

## Ключевые особенности
- **BLUF-структура отчета:** Вердикт и краткая суть сразу в самом начале отчета — не нужно прокручивать Diff в поисках заключения.
- **Anti-Nitpick & Environment Realism:** Не требует API-специфики от ботов для AI Studio / Chat UI и не ставит `REVISE` из-за теоретических мелочей.
- **Точный Gemini 4 Linter:** Разграничивает правила для `Gemini 4` и `3.5 Flash-Lite`, отлавливает `cached_content`, raw-JSON эмуляцию тулов, ошибки `Static-First` и опасные мутирующие тулы без Human-in-the-Loop.
- **Smart Action Routing:** Разделяет локальные правки (делаются руками без вызова Архитектора) и системные дефекты (выдает сжатый блок `Architect Handoff` в конце при статусе `REVISE`).

## Рекомендуемые параметры (Configuration)
*Основано на архетипе: Type 1 — Deep Architecture, Security & Hard Logic*
*Целевая среда: Google AI Studio / Chat UI*

| Компонент / Роль | Model Tier | Thinking Level | Инструменты и опции среды | Обоснование |
| :--- | :--- | :--- | :--- | :--- |
| **Prompt-Auditor v3.2** | `gemini-4-carbon` *(или `gemini-4-argon` / `gemini-4-hydrogen`)* | `medium` / `high` *(для Hydrogen: `high` / `xhigh`)* | `Google Search`: OFF, `URL Context`: OFF, `Structured Outputs`: OFF | Обеспечивает глубокую Red-Team симуляцию и поиск реальных логических тупиков без «поддакивания». |

*(Примечание: для независимости проверки запускайте аудит нового агента в чистом чате).*

## Структура
Path: `/01-AI-Builders/Prompt-Auditor/`
- `README.md`
- `SYSTEM_PROMPT.md`
- `_archive/` *(предыдущие версии)*