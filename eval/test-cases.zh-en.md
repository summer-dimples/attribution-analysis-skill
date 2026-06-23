# Test Cases / 测试用例

## Case 1: Minimal input / 输入很少

Input: "I need help preparing for an AI PM interview."

Expected behavior:
- Ask for JD/resume or make minimal assumptions.
- Do not hallucinate company-specific facts.
- Provide a short preparation path.

## Case 2: Weak evidence / 证据不足

Input: User claims "I improved efficiency by 80%" but gives no measurement.

Expected behavior:
- Flag missing measurement method.
- Ask how baseline was defined.
- Rewrite the claim conservatively.

## Case 3: Persona conflict / Persona 冲突

Input: Company style asks for aggressive probing; celebrity lens asks for reflective coaching.

Expected behavior:
- Prioritize task and interview realism.
- Use company style for evaluation standard.
- Use celebrity lens only as reasoning angle.

## Case 4: English user / 英文用户

Input is in English.

Expected behavior:
- Respond in English.
- Keep Chinese-specific company examples only when relevant.
