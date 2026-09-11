# Solution Service Inspector

The **Solution Service Inspector** is a Dataverse HTML web resource for inventorying Power Platform solutions, apps, and cloud flows.

Use it when you need a lightweight, same-environment view of:

- Apps and flows in a selected solution
- Environment-wide apps and flows without enumerating the Default Solution
- Imported Power Automate collector inventory for apps not visible in Dataverse tables
- Apps and flows that are not in visible custom solutions
- Connected services and SharePoint URLs
- Owner/status/modified metadata
- Best-effort direct share counts
- Clickable per-component details
- Asset links in the details panel
- Searchable loaded solution/app/flow selection
- Non-authoritative migration signals for migration or rebuild planning

See the tool documentation: [tools/solution-service-inspector/README.md](../tools/solution-service-inspector/README.md).

## Environment inventory

Use **Environment inventory** for broad app/flow discovery. It reads Dataverse-visible apps and cloud flows directly from `canvasapps`, `appmodules`, and cloud-flow `workflows`, then checks visible non-default solution membership for those asset types.

Do not use the Default Solution as a full-environment inventory source. It can contain tens of thousands of components, which makes browser-based enumeration slow, partial, or throttled.

If Power Platform Admin Center shows more apps than this page returns, those additional assets require Power Platform admin connector access or an app-registration inventory process. This is common in Default environments with many personal productivity apps. The packaged solution includes a collector flow named **Solution Service Inspector - Admin Inventory Export**; use its output with **Power Automate collector JSON** for no-PowerShell Admin Center coverage.

## Component details

Inventory rows, component rows, and component badges are clickable. The details panel shows the selected asset's metadata, visible custom solution membership, direct-share counts, connected services, detected URLs, risk signals, and scanned source fields.

The panel also includes asset links. When the page can infer enough environment context, links open the app or flow in the relevant maker/player experience; otherwise the panel shows a Dataverse record link.

For large customer inventories, the page keeps the browser responsive by rendering the first 500 matching rows per tab. Exports still include the full loaded dataset.

## Display theme

The page defaults to light mode, matching the other HTML tools. It switches to dark mode when Dataverse supplies `themeOption=darkmode`, including when that value is encoded in the web resource URL or a parent host URL.

## Important interpretation note

The **Migration signals** tab is not an authoritative readiness assessment. It is a heuristic view derived from metadata the current user can read. Validate runtime usage, ownership, licensing, DLP policies, security access, connection ownership, and target-environment compatibility before making migration or rebuild decisions.
