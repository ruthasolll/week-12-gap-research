# Day 2 Thread — Agent & Tool Use Internals

1/ Problem I ran into:

I built a system with “tools” (MCP server + schemas), but the LLM almost never produced valid tool calls.

Instead, it:
- wrote normal text
- or produced malformed JSON
- or ignored tools entirely

2/ My assumption was wrong.

I thought tool-use was something the model *does internally*.

But after debugging Week 10, I realized:
👉 the model was never actually being put into a real tool-use setting

3/ Key correction:

Tool use is NOT a special reasoning mode.

It is just token prediction under constraints.

The model is always doing:
P(next token | prompt)

4/ So what is a “tool call”?

It’s just a high-probability structured sequence like:

{
  "name": "send_email",
  "arguments": {...}
}

If this pattern is not strongly favored → tool use fails.

5/ Why my system failed

In my setup:
- tool schemas were not strictly structured
- no few-shot tool examples
- no decoding constraints (JSON enforcement)
- model defaulted to natural language

So:
👉 P(text) >> P(tool-call)

6/ Important diagnostic insight:

If the output is:
- unstructured
- not parseable
- not schema-valid

Then tool use did NOT happen.

It was just normal text generation.

7/ What real tool use requires

To reliably trigger tool calls:

- strict JSON schemas (not human docstrings)
- few-shot tool-call examples
- constrained decoding (low temperature / JSON mode)

These shift probability mass toward structured outputs.

8/ Final insight

What I called “agent behavior” was actually:

👉 deterministic orchestration + text generation

Not:
👉 model-driven tool execution
