---
name: usage
description: Track session token usage and estimate costs. Shows input/output tokens, estimated cost, and quota remaining (if known).
license: MIT
compatibility: Python 3.12+
user-invocable: true
allowed-tools:
  - bash
  - read_file
  - grep
---

# Usage Tracking Skill

Track your session's token consumption and estimate costs.

## Usage

```
/usage
```

Output:

```
┌─────────────────────────────────────────────────────────────┐
│ SESSION USAGE SUMMARY                                       │
├─────────────────────────────────────────────────────────────┤
│ Input Tokens:     45,230                                   │
│ Output Tokens:    12,450                                   │
│ Total Tokens:      57,680                                   │
├─────────────────────────────────────────────────────────────┤
│ Estimated Cost (devstral-2):  ~$0.04                       │
│ Estimated Cost (devstral-small): ~$0.01                     │
├─────────────────────────────────────────────────────────────┤
│ Pricing Reference:                                          │
│ devstral-2:     $0.40/1M input, $2.00/1M output            │
│ devstral-small: $0.15/1M input, $0.60/1M output            │
└─────────────────────────────────────────────────────────────┘

Session started: 2026-01-15 10:30:00
Current model: devstral-2
Background agents spawned: 3 (Achates x2, Agrippa x1)
```

## When to Use

- Before starting a large task: "How much quota do I have left?"
- During long sessions: "What's my current usage?"
- Before background agents: "What will 5 parallel agents cost?"
- After expensive operations: "Did that just use a lot of tokens?"

## Cost Estimation Formula

```
Cost = (input_tokens / 1,000,000 × input_price) + (output_tokens / 1,000,000 × output_price)
```

Example (devstral-2):
- Input: 100,000 tokens × $0.40/1M = $0.04
- Output: 30,000 tokens × $2.00/1M = $0.06
- Total: $0.10

## Tips to Reduce Usage

1. **Switch models strategically**
   - Simple grep: devstral-small
   - Complex reasoning: devstral-2

2. **Use background agents sparingly**
   - Each agent adds to the total
   - Combine related tasks when possible

3. **Avoid re-reading large files**
   - Use grep to find specific sections
   - Cache context you'll need again

4. **Clear context when switching topics**
   - Use `/clear` to reset session
   - Prevents context pollution

5. **Use read_file with offset/limit**
   - Don't read entire files
   - Read only what you need