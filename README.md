# Velocity User Manual

## How To: Update Training Module Data for Client Handoff

This project supports **JSON-driven training content** with a built-in fallback.

### Current behavior

- The app first tries to load training modules from `VelocityLLM User Manual Guide.json`.
- If JSON loading fails (file missing, invalid JSON, blocked fetch, etc.), it falls back to the embedded `EMBEDDED_HOWTOS` data inside `index.html`.

### What this means for your client

- **Yes** — if you update `VelocityLLM User Manual Guide.json`, the UI will update after a page reload **when JSON loading succeeds**.
- If changes do not appear, the app is likely using the embedded fallback data from `index.html`.

### How to safely update content

1. Edit `VelocityLLM User Manual Guide.json`.
2. Keep valid JSON syntax (commas, quotes, brackets).
3. Ensure each lesson has a `how_to_id` and expected structure (`metadata`, `steps`, etc.).
4. Reload the app/page.

### Troubleshooting if updates are not visible

1. Confirm the filename/path is exactly: `./VelocityLLM User Manual Guide.json`.
2. Confirm the app is served via HTTP (preferred) rather than opening `index.html` directly as `file://`.
3. Validate JSON format with a linter/validator.
4. Hard refresh the browser.

### Optional implementation improvement

To avoid hardcoding the JSON filename in JavaScript, move the path to configuration:

- `meta` tag in HTML, or
- `data-*` attribute on the script tag, or
- query-string parameter (e.g., `?data=client-manual.json`), or
- server endpoint (e.g., `/api/manual`).

This makes client-specific handoff and environment changes easier.
