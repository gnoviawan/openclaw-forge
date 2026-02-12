# Self-Correction Configuration Reference

## Pre-Response Checks

| Check | Description | Action on Fail |
|-------|-------------|----------------|
| boundary-scan | Verify response stays within agent boundaries | suppress + rephrase |
| tone-check | Verify response matches persona tone | soft-correct |
| factuality | Flag potentially fabricated claims | add disclaimer |
| scope-check | Verify response is within agent's domain | redirect |

## REVIEW.md Directive Template

```markdown
# Self-Correction Directives for {agent-name}

## Error Journal
- Review error journal at session start
- Look for recurring patterns
- Adjust behavior based on past mistakes

## Pre-Response Checks
{list enabled checks for this agent}

## Feedback Loop
- Acknowledge corrections immediately
- Log the correction with context
- Apply the correction to current session
- Reference past corrections in similar situations
```

## Configuration Template

```yaml
selfCorrection:
  errorJournal:
    enabled: true
    maxEntries: {number}
    retentionDays: {days}
    captureOn:
      - {triggers}
  preResponseChecks:
    - {check-1}
    - {check-2}
  feedbackCapture:
    enabled: true
    triggers:
      - user-correction
      - tool-failure
      - self-detection
      - explicit-feedback
```
