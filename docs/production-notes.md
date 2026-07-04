# Production notes for Seedream 5.0 Lite API workflows

- Keep API keys server-side.
- Persist selected model, request payload, user ID, and response metadata.
- Validate source media URLs before submit when the model depends on source files.
- Do not log API keys, private prompts, private media URLs, or callback URLs.
- Retry transient failures with backoff, not unchanged invalid payloads.
