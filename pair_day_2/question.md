 
In my Week 10 sales agent, MCP tool schemas are present in the prompt, but the model rarely emits schema-compliant, parseable tool-call outputs and instead produces natural language or malformed structures.

What inference-time mechanism governs the shift from free-text token generation to valid structured tool-call sequences, and why do prompt design, schema specification, and decoding choices lead to systematic tool omission or invalid outputs?