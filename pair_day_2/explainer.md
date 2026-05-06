 
# explainer.md

## What “tool use” actually is at inference time (and why your MCP tools are ignored)

### The Question

In your Week 10 project, you built an MCP server with tool schemas, but the LLM never invokes them unless you explicitly orchestrate execution. You describe your system as “agent + tool use,” but cannot explain the mechanism.

Specifically:
- What token sequence represents a tool call?
- How are tool schemas injected into the model context?
- How does the runtime distinguish tool calls from normal text?

---

## Why this matters

Right now, your system behaves like a **deterministic pipeline**, not a model-driven agent.

Closing this gap determines whether:
- your tools are actually consumable by the model  
- your schema design is valid for inference-time conditioning  
- your orchestrator is a deliberate abstraction or a workaround  

---

## The load-bearing mechanism

> **Tool use = constrained structured generation + post-hoc parsing**

There is no internal “function execution” inside the model.

At inference time:

Latency ≈ Prefill(prompt_tokens) + Decode(output_tokens)

and

Output ≈ argmax P(tokens | prompt + tool schema)

A tool call is simply a **high-probability structured token sequence** (e.g., JSON) that the runtime interprets.

---

## 1. What happens at the token level

LLMs generate tokens autoregressively:

P(t₁, t₂, ..., tₙ) = ∏ P(tᵢ | t<i)

A “tool call” is just a sequence like:

{
  "name": "send_email",
  "arguments": {
    "recipient": "john@example.com"
  }
}

At the token level, this is:

{ → "name" → ":" → "send_email" → "," → ...

There is:
- no API call inside the model  
- no execution  
- no symbolic reasoning  

👉 Only probability over tokens.

---

## 2. How tool schemas are injected

Tool schemas are serialized into the prompt.

In systems like OpenAI function calling or Claude tool use, the runtime constructs something equivalent to:

You can use the following tools:

Tool: send_email  
Description: Sends an email  
Parameters:
- recipient: string  
- body: string  

When appropriate, output a JSON function call.

So internally:

> Tool definitions = prompt tokens

They influence the model through standard attention mechanisms.

---

## 3. How the parser distinguishes tool calls

After generation, the runtime performs:

1. String parsing (e.g., JSON decoding)  
2. Schema validation  
3. Dispatch logic  

Pipeline:

LLM → token sequence → parser → schema match → tool execution

If output matches expected structure → execute tool  
Else → treat as normal text  

👉 The model does not execute anything. The system does.

---

## 4. Why your MCP tools are not used

Your current schemas are likely:

- optimized for human readability  
- unstructured or verbose  
- missing strict parameter definitions  

This causes:

> P(natural language) > P(structured tool call)

So the model defaults to normal text instead of tool usage.

---

## 5. What “choosing a tool” actually means

It is not:

“the model decides to call a function”

It is:

“the model assigns higher probability to a structured output pattern than to free text”

So tool selection is a **probability distribution shaping problem**.

---

## 6. What you should change (technical + actionable)

Your goal is to **increase the probability mass on valid tool-call token sequences**.

---

### 6.1 Convert tools into strict schemas (not docstrings)

❌ Current (human-oriented):

"This tool can be used to send emails to customers..."

✅ Required (model-oriented):

{
  "name": "send_email",
  "description": "Send an email to a recipient",
  "parameters": {
    "type": "object",
    "properties": {
      "recipient": { "type": "string" },
      "body": { "type": "string" }
    },
    "required": ["recipient", "body"]
  }
}

Why this works:
- Matches model training distribution (JSON/code)
- Reduces ambiguity in token prediction
- Enables structured decoding

---

### 6.2 Add explicit output constraints

Without constraints:

P(text) > P(JSON)

You must enforce:

"If a tool is relevant, respond ONLY with a JSON object. Do not output natural language."

This reshapes decoding behavior.

---

### 6.3 Provide few-shot examples (critical)

Example:

User: Send email to John  
Assistant:
{
  "name": "send_email",
  "arguments": {
    "recipient": "john@example.com",
    "body": "Hello"
  }
}

Why this matters:
- Anchors early tokens ("{", "name", etc.)
- Strongly increases likelihood of correct structure
- Teaches when to trigger tools

---

### 6.4 Use schema-constrained decoding (if available)

Modern APIs allow:
- enforcing JSON validity
- restricting outputs to schema-compliant tokens

Effect:

P(invalid outputs) → 0

---

### 6.5 Separate reasoning from action

Instead of:

Model → action directly

Use:

Step 1: reasoning  
Step 2: structured action  

Example:

Thought: I should send an email  
Action:
{
  "name": "send_email",
  ...
}

This improves:
- reliability
- interpretability
- tool selection accuracy

---

### 6.6 Add explicit tool selection rules

Example:

Use send_email ONLY when:
- user explicitly asks to send a message

Without this, the model cannot learn when to trigger tools.

---

### 6.7 Add observability (debugging)

Track:
- tool_call_rate (% structured outputs)
- parse_success_rate
- tool vs text ratio

This lets you verify whether your prompt changes are working.

---

## 7. Adjacent concepts (brief)

### Prompt conditioning
Tool use depends entirely on how strongly the prompt biases structured output.

### Decoding strategies
Lower temperature → more reliable structured outputs

### KV cache
Tool schemas remain in memory across generation and influence all tokens.

---

## 8. Mental model

> The model does not use tools.  
> It generates tokens that resemble tool calls.  
> The system executes them if they match a schema.

---

## 9. Bottom line

- Tool use = structured token generation + parsing  
- Schemas = prompt-level conditioning  
- Execution = external system logic  

Your current system is:

> manual orchestration

A true agent system requires:

> model-driven structured generation

---

## Sources

1. Vaswani et al. (2017) — Attention Is All You Need  
https://arxiv.org/abs/1706.03762  

2. OpenAI Function Calling Documentation  
https://platform.openai.com/docs/guides/function-calling  

3. Anthropic Tool Use Documentation  
https://docs.anthropic.com/en/docs/build-with-claude/tool-use  