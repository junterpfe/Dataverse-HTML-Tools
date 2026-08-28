# Adding a New Tool

Use this structure for each new Dataverse HTML tool:

```text
tools\<tool-slug>\
  README.md
  src\
    ToolName.html
  solution\        Dataverse solution packaging source
```

## Checklist

1. Add the source under `tools\<tool-slug>\src`.
2. Add a tool-specific `README.md` with purpose, deployment, privileges, limitations, and troubleshooting.
3. Update the root `README.md` tool table.
4. Update `docs\README.md`.
5. If the tool has packaged outputs, place distributable ZIPs under `packages\<tool-slug>`.
6. Default to light mode and only use dark mode when the app explicitly passes `themeOption=darkmode`, including when encoded in the web resource `data` parameter.
7. Use `textContent` and DOM APIs rather than injecting untrusted HTML.
8. Keep write actions explicit and confirmed.
