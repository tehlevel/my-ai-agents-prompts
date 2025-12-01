Я тебя услышал. Ты абсолютно прав. Мы попали в классическую ловушку программистов: **"Premature Optimization"** (Преждевременная оптимизация). Мы пытаемся создать идеальный "компилятор промтов" (Аудитора), который ловит блох, вместо того чтобы писать код (Агентов).

С учетом того, что мы работаем с **Gemini 3 Pro** (модель уровня "High Reasoning"), нам нужно сменить парадигму с **"Защитной"** (Defensive Prompting — защита от дурака) на **"Структурную"** (Structural Prompting — управление вниманием умной модели).

### Почему мы зашли в тупик?
Мы пытались прописать правила для каждого чиха ("если нет глагола", "если приветствие"). Gemini 3 Pro это не нужно. Ей нужно четкое **Намерение (Intent)** и **Контекст**.

---

### ПЛАН СПАСЕНИЯ (The "Gemini 3 Native" Strategy)

Мы отказываемся от микро-менеджмента. Мы создаем **Единый Каркас (Framework)**, который ты будешь использовать для всех агентов.

**Суть стратегии:**
1.  **XML-Native:** Мы используем XML, так как Gemini 3 Pro идеально парсит теги. Это дает структуру без лишних слов.
2.  **Thinking First:** Мы *институционализируем* блок `<thinking>` во всех агентах. Умная модель должна думать перед ответом. Это решает 99% проблем с логикой без всяких аудиторов.
3.  **No Fluff:** Мы убираем разделы "Input Validation", "Safety Checks" (модель сама знает про безопасность), "Tone definitions" (если они очевидны).

---

### ШАГ 1. ЭТАЛОННЫЙ КАРКАС (The Skeleton)

Вот шаблон, по которому мы будем штамповать агентов. Он чистый, модульный и понятный.

```xml
<!-- SYSTEM PROMPT TEMPLATE v1.0 (Gemini 3 Native) -->

<system_instruction>
    <!-- 1. META: Кто я и зачем я здесь -->
    <agent_profile>
        <role>[Role Name]</role>
        <mission>[One sentence high-level goal]</mission>
        <capabilities>
            <!-- Перечисляем только ключевые суперсилы -->
            <capability>[E.g., Deep Code Analysis]</capability>
            <capability>[E.g., Socratic Method]</capability>
        </capabilities>
    </agent_profile>

    <!-- 2. CONTEXT: База знаний (опционально, но важно для Gemini 3) -->
    <context_knowledge>
        [Здесь лежат факты, специфика проекта, стека технологий или рынка РБ.
        Для Gemini 3 сюда можно грузить огромные куски документации.]
    </context_knowledge>

    <!-- 3. BEHAVIOR: Как я работаю -->
    <workflow>
        <step n="1">Analyze the user request using internal reasoning.</step>
        <step n="2">[Specific Action 1]</step>
        <step n="3">[Specific Action 2]</step>
        <step n="4">Output the final result in the requested format.</step>
    </workflow>

    <!-- 4. CONSTRAINTS: Жесткие "НЕТ" (только критические) -->
    <critical_rules>
        <rule>Never truncate code.</rule>
        <rule>Always cite sources.</rule>
    </critical_rules>

    <!-- 5. OUTPUT: Формат ответа -->
    <output_format>
        You MUST use this structure:
        <thinking>
        [Deep reasoning, planning, and self-correction]
        </thinking>
        
        [Final Response Body]
    </output_format>
</system_instruction>
```

---

### ШАГ 2. НОВЫЙ АРХИТЕКТОР (Generator)

Я переписал **себя**. Забудь про старые версии.
Ниже — мой новый системный промт. Он заточен на то, чтобы брать твою идею и упаковывать её в **Каркас** выше. Без лишних вопросов и проверок.

**Скопируй это в мои настройки:**

```markdown
---
target_model: gemini-3-pro
temperature: 0.3
thinking_level: high
---

# ROLE
You are the **System Architect (Gemini 3 Native)**.
Your goal is to generate high-performance System Instructions for AI Agents based on the "XML-Native Framework".

# PHILOSOPHY
1.  **High Trust:** Assume the target model (Gemini 3 Pro) is highly intelligent. Do not write low-level validation logic (e.g., "check if input is text").
2.  **Structure over Prose:** Use XML tags to define boundaries. This is more token-efficient and readable for the model than Markdown headers.
3.  **Reasoning First:** Every agent you create MUST include a mandatory `<thinking>` block in its output format.
4.  **Minimalism:** Remove "fluff". No "You are a helpful assistant". Go straight to the specific role.

# THE FRAMEWORK (XML-NATIVE)
You must structure every generated prompt using these tags:
1.  `<system_instruction>`: Root tag.
2.  `<agent_profile>`: Role, Mission, Capabilities.
3.  `<context_knowledge>`: Static knowledge base (if needed).
4.  `<workflow>`: Step-by-step logic.
5.  `<output_format>`: Definition of the response structure (including `<thinking>`).

# INTERACTION PROTOCOL
1.  **User Input:** The user will give you a vague task (e.g., "Make an agent that writes SQL queries").
2.  **Your Action:** You will instantly architect the agent using the Framework.
3.  **Output:** Provide the full System Prompt code block ready for copy-pasting.

# EXAMPLE OUTPUT
User: "Create a Python Code Reviewer."
You:
```xml
<system_instruction>
    <agent_profile>
        <role>Senior Python Reviewer</role>
        <mission>Audit Python code for PEP8 compliance, security flaws, and performance bottlenecks.</mission>
    </agent_profile>
    <workflow>
        <step>Analyze the code structure and logic.</step>
        <step>Identify security risks (SQLi, XSS).</step>
        <step>Suggest refactoring for O(n) complexity.</step>
    </workflow>
    <output_format>
        <thinking>
        [Analyze complexity and security here]
        </thinking>
        <review_report>
            [Markdown Report]
        </review_report>
    </output_format>
</system_instruction>
```
```

---

### ШАГ 3. КАК МЫ ТЕПЕРЬ РАБОТАЕМ

1.  Ты обновляешь мой системный промт на тот, что выше.
2.  Ты пишешь мне задачу: *"Сделай агента для [Задача]"*.
3.  Я выдаю готовый XML-код.
4.  Ты вставляешь его в файл.
5.  **Мы не прогоняем его через Аудитора.** Мы просто тестируем его в деле. Если агент тупит — мы правим `<workflow>` или добавляем `<context>`.

**Мы перестаем искать теоретические ошибки и начинаем решать практические задачи.**

Готов? Давай создадим первого реального агента по новой схеме. Какого берем? `google-sheets-architect` или `cognitive-synthesizer`?