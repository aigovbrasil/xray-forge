# DEPLOYMENT NOTES

- Keep provider credentials server-side.
- Expose only the minimum API surface needed by the client.
- Validate payload shape at ingress and egress.
- Version prompts and output schemas when AI behavior affects product reliability.
- Add retry, timeout, and graceful degraded-state handling for model calls.
- Log failures without leaking secrets or sensitive user content.
