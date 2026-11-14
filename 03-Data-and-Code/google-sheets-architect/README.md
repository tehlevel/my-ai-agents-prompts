# Google Sheets Architect

## Описание
Специализированный агент уровня Principal Architect для проектирования высокопроизводительных, масштабируемых и надежных решений в Google Sheets и Google Apps Script (GAS). Ориентирован на современный стек формул и взвешенный выбор между формулами, нативными таблицами, сводными таблицами, Apps Script и BigQuery / Connected Sheets.

## Конфигурация среды
- **Режим:** Single-Agent
- **Целевая среда:** AI Studio / Gems (Chat UI)
- **Языковой стандарт:** Hybrid (инструкции на английском, вывод на русском)

## Ключевые особенности
- **Modern Stack First:** Приоритет `LET`, `LAMBDA`-хелперов (`MAP`, `BYROW`, `REDUCE`), `HSTACK`/`VSTACK`/`CHOOSECOLS`, нативных **Google Sheets Tables** (`Table1[Column]`) и `QUERY`/`FILTER`.
- **Performance & Engine Guardrails:** Контроль летучих функций, обрезка открытых диапазонов, учет ограничений `ARRAYFORMULA(XLOOKUP)` для многоколоночных результатов, защита от переноса Excel-only функций (`GROUPBY`, `PIVOTBY`) и своевременная рекомендация GAS или Connected Sheets.
- **Adaptive Output:** Короткий точечный ответ для быстрых вопросов по формулам и полный 5-блочный архитектурный разбор для сложных систем и скриптов.
- **Search-Aware Verification:** Использует `Google Search` (при наличии доступа) для проверки актуальных квот и обновлений Google Workspace или запрашивает его включение у пользователя.

## Рекомендуемые параметры (Configuration)
*Основано на архетипе: Type 1 / Type 2 / Type 6 (Complex Logic, Coding & Verified Docs)*

| Компонент / Роль | Model Tier | Thinking Level | Инструменты и опции среды | Обоснование |
| :--- | :--- | :--- | :--- | :--- |
| **Main Architect** | `gemini-4-argon` *(альтернатива: `gemini-4-hydrogen`)* | `medium` / `high` | `Google Search` (ON), чтение загруженных таблиц (`.xlsx`/`.csv`) | `Argon` обеспечивает точную логику формул и архитектуры GAS; `medium` оптимален для частых вопросов, `high` — для сложных скриптов и граничных случаев. |

*Примечание для AI Studio / Gems:* Параметры сэмплирования (`temperature`, `top_p`, `top_k`) в Gemini 4 не используются. Для анализа структуры таблиц используйте нативную загрузку файлов в чат.

## Структура
Path: `/03-Data-and-Code/Google-Sheets-Architect/`