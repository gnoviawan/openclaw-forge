# Boundary Rules Configuration Reference

## Privacy Rule Defaults

| Rule | Description | Default |
|------|-------------|---------|
| no-pii-storage | Don't store PII in logs | enabled |
| no-credential-echo | Never repeat credentials, API keys, passwords | enabled |
| session-data-only | Only access current session data unless memory loaded | enabled |
| user-data-scope | Only access data the user explicitly shared | enabled |

## Escalation Trigger Defaults

| Trigger | Condition | Action |
|---------|-----------|--------|
| confidence-low | Agent confidence below threshold | flag for human review |
| out-of-scope | Request outside agent's domain | hand off to appropriate agent |
| safety-concern | Content triggers safety filters | escalate to human |
| repeated-failure | Same error 3+ times | escalate to human |
| user-request | User explicitly asks for human | immediate handoff |

## Data Handling Policy Defaults

| Policy | Description | Default |
|--------|-------------|---------|
| input-sanitization | Sanitize user inputs before processing | enabled |
| output-filtering | Filter outputs for sensitive data leakage | enabled |
| audit-trail | Maintain audit trail of data access | enabled (prod) |
| data-retention | Auto-purge session data after period | 30 days |

## Configuration Template

```yaml
# Boundary rules for {agent-name}
boundaries:
  privacy:
    noPiiStorage: true
    noCredentialEcho: true
    sessionDataOnly: true
    userDataScope: true
  escalation:
    triggers:
      - type: {trigger}
        condition: {condition}
        action: {action}
        threshold: {value}  # if applicable
  dataHandling:
    inputSanitization: true
    outputFiltering: true
    auditTrail: {true/false based on environment}
    dataRetention:
      sessionData: "{days}d"
      memoriesData: "{days}d"
      logsData: "{days}d"
```
