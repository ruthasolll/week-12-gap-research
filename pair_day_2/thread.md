 
# Day 2 Thread — Agent & Tool Use Internals

1/ My LLM had tools… but didn’t really use them correctly.

It kept producing normal text instead of structured tool calls.

2/ Tool use is NOT a special capability.

It’s just next-token prediction:
- text tokens vs structured tokens

3/ A tool call only happens when structured tokens become more probable than natural language.

Example: `{ "name": ... }`

4/ Why it breaks:
- weak prompts → model ignores structure
- unclear schemas → no strong pattern
- no examples → no guidance
- high randomness → broken JSON

5/ Key insight:

If output is not schema-compliant and parseable, then tool use did NOT happen.

6/ Tool reliability is not magic.

It’s prompt design + token probability + decoding behavior.

Full write-up: [link]