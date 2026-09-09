# Solution Service Inspector

The **Solution Service Inspector** is a Dataverse HTML web resource for inventorying Power Platform solutions, apps, and cloud flows.

Use it when you need a lightweight, same-environment view of:

- Apps and flows in a selected solution
- Environment-wide apps and flows without enumerating the Default Solution
- Apps and flows that are not in visible custom solutions
- Connected services and SharePoint URLs
- Owner/status/modified metadata
- Best-effort direct share counts
- Non-authoritative migration signals for migration or rebuild planning

See the tool documentation: [tools/solution-service-inspector/README.md](../tools/solution-service-inspector/README.md).

## Environment inventory

Use **Environment inventory** for broad app/flow discovery. It reads apps and cloud flows directly from `canvasapps`, `appmodules`, and cloud-flow `workflows`, then checks visible non-default solution membership for those asset types.

Do not use the Default Solution as a full-environment inventory source. It can contain tens of thousands of components, which makes browser-based enumeration slow, partial, or throttled.

## Display theme

The page defaults to light mode, matching the other HTML tools. It switches to dark mode when Dataverse supplies `themeOption=darkmode`, including when that value is encoded in the web resource URL or a parent host URL.

## Important interpretation note

The **Migration signals** tab is not an authoritative readiness assessment. It is a heuristic view derived from metadata the current user can read. Validate runtime usage, ownership, licensing, DLP policies, security access, connection ownership, and target-environment compatibility before making migration or rebuild decisions.
