<thinking>
1. Analysis:
   - Conflict: The "Few-Shot Example" for the Calculator prompt has English Input ("You are a Calculator...") but Russian Output ("# 🛡️ ОТЧЕТ QA v7.1"). This contradicts the rule "Output Report: ALWAYS in the same language as the User Input." (-20 pts).
   - Conflict: The "Few-Shot Example" for the Non-Prompt ("Water flows downhill") includes a `<thinking>` block. However, the instruction "*(You MUST start with the thinking block)*" is explicitly placed only under "TEMPLATE B", not Template A. This creates ambiguity on whether Template A requires internal monologue. (-20 pts).
   - Ambiguity: The "Gatekeeper" logic says "IF < 2 components found -> Output TEMPLATE A". It does not explicitly say "STOP" or "Do not calculate score". While implied, explicit constraints are safer. (-5 pts).
2. Calculation: 100 - 20 - 20 - 5 = 55.
3. Decision: Score 55 < 95, so Render Stress Test.
</thinking>

# 🛡️ QA REPORT v7.1

## 📊 Score: 55/100

## 🚨 Logic Flaws
### 1. Example vs Rule Conflict (Language) (-20)
*   **Conflict:** The Rule states: "Output Report: ALWAYS in the same language as the User Input." However, the Few-Shot Example shows an English input ("You are a Calculator...") resulting in a Russian output report.
*   **Result:** The model may get confused and output in a different language (e.g., Russian) even when the user inputs English, prioritizing the few-shot pattern over the system instruction.
*   **Fix:** Change the Few-Shot Example input to Russian ("Ты - Калькулятор...") OR change the Example output to English.

### 2. Example vs Rule Conflict (Thinking Block) (-20)
*   **Conflict:** The instruction "*(You MUST start with the thinking block)*" is nested under **TEMPLATE B**. It is absent from **TEMPLATE A**. However, the Few-Shot Example for Template A ("Water flows downhill") *includes* a thinking block.
*   **Result:** The model may omit the thinking block for Template A (following the instruction placement) or include it (following the example), leading to inconsistent behavior for invalid inputs.
*   **Fix:** Move the "Thinking Process" instruction to the global "LANGUAGE PROTOCOL" or "WORKFLOW" section so it applies to ALL templates.

### 3. Weak Constraint (Gatekeeper) (-5)
*   **Conflict:** The Gatekeeper says "Output TEMPLATE A". It does not explicitly forbid calculating a score or generating the rest of the report.
*   **Result:** The model might output Template A and then continue to try and audit the text anyway, or hallucinate a score of 0.
*   **Fix:** Add "Output TEMPLATE A and **STOP generation**."

---
## 🧪 Stress Test
**Scenario:** User inputs a valid English prompt: "You are a poet. Write a poem."
**Failure:**
"# 🛡️ ОТЧЕТ QA v7.1
## 📊 Оценка: 100/100..."
*(The model outputs in Russian because it mimics the Few-Shot Example where English Input -> Russian Output).*

---
## ✅ Checklist
- [ ] Align Few-Shot Examples with the Language Protocol (English Input -> English Output).
- [ ] Make the `<thinking>` block mandatory globally, not just for Template B.
- [ ] Add a "STOP" command to the Gatekeeper's Template A path.