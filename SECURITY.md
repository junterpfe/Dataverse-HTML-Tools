# Security

These tools are intended for admin-owned Dataverse/model-driven app environments.

## Zero Trust principles

- **Use the signed-in user context.** The tools run through `Xrm.WebApi` and inherit the current user's Dataverse privileges.
- **Do not treat client-side checks as enforcement.** UI gating and hidden buttons are convenience only; Dataverse roles and privileges are the enforcement boundary.
- **Minimize data reads.** Query only the fields needed for the view or action. For example, Flow Dependency Viewer checks environment-variable value existence for table indicators and loads a current value only after the user opens the editor for that specific variable.
- **Do not expose secrets.** Do not pass secrets in URL parameters, logs, docs, browser automation, or bulk data queries. Secret environment-variable current values are not displayed.
- **Avoid untrusted HTML injection.** Prefer DOM creation and `textContent`. Do not use `innerHTML`, `eval`, or third-party script/CDN dependencies unless there is a reviewed, documented need.
- **Confirm write actions.** Keep explicit confirmations for role changes, team membership changes, flow state changes, and environment-variable value updates.
- **Prefer managed deployment for downstream environments.** Use managed solutions for test/production and restrict who can import or customize these web resources.

## Recommended operational controls

- Put the tools in a dedicated admin model-driven app.
- Grant access only to administrators who already have the corresponding Dataverse privileges.
- Review browser/dev-tool logs before using the tools for secret-handling workflows.
- Add Dataverse audit logging for write actions if the tools become production-governed utilities.
