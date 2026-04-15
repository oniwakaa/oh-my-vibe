# Rate Limits and Quotas

## Mistral API Quotas

Vibe CLI uses the Mistral API. Quotas vary by plan:

| Plan | Devstral-2 | Devstral-Small | Rate Limit | Cost |
|------|------------|----------------|------------|------|
| Experiment | ~50 requests | ~100 requests | Aggressive | Free |
| Le Chat Pro | ~500 requests | ~1000 requests | Moderate | €20/mo |
| API Direct | Unlimited | Unlimited | Pay-per-use | $0.40/$2.00 per 1M tokens |

### Checking Your Quota

1. Visit https://console.mistral.ai
2. Navigate to "Usage" or "Quotas"
3. View remaining requests/tokens

### When You Hit Limits

**Symptoms:**
- CLI shows "generating" indefinitely
- Error: "rate limit exceeded"
- Error: "quota exceeded"

**Solutions:**

1. **Switch to Devstral-Small** (cheaper, more quota)
   ```
   /model devstral-small
   ```

2. **Wait for reset**
   - Most quotas reset hourly or daily
   - Check console for reset times

3. **Use background agents efficiently**
   - Parallel agents share the quota
   - Sequential agents double quota usage

4. **Upgrade plan**
   - Le Chat Pro: https://console.mistral.ai/subscription
   - API Direct: Use pay-per-use API key

## EXA API (Web Search)

oh-my-vibe uses EXA for web search:

| Tier | Requests | Cost |
|------|----------|------|
| Free | 1,000/month | Free |
| Pro | 10,000/month | $29/mo |
| Enterprise | Unlimited | Custom |

### Getting EXA Key

1. Visit https://exa.ai
2. Create account
3. Generate API key
4. Add to `~/.vibe/.env`:
   ```
   EXA_API_KEY=your_key_here
   ```

## Context7 (Library Docs)

No API key required. Free to use.

## grep_app (OSS Code Search)

No API key required. Free to use.

## Usage Tracking in Sessions

To track token usage during a session:

```
> How many tokens have I used this session?

[Hercules checks session metrics]
You've used approximately:
- Input tokens: 45,000
- Output tokens: 12,000
- Total: 57,000 tokens

At Devstral-2 pricing ($0.40/$2.00), this session cost ~$0.04.
```

## Best Practices

| Situation | Recommendation |
|-----------|---------------|
| Quick grep/search | Use `devstral-small` |
| Complex reasoning | Use `devstral-2` |
| Large codebase analysis | Use background agents sparingly |
| Many parallel tasks | Space out over time to avoid burst limits |
| Production use | Use API Direct plan |