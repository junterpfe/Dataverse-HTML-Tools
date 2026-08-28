# Solution Service Inspector

The **Solution Service Inspector** is a Dataverse HTML web resource for inventorying Power Platform solutions, apps, and cloud flows.

Use it when you need a lightweight, same-environment view of:

- Apps and flows in a selected solution
- Apps and flows that are not in a custom solution
- Connected services and SharePoint URLs
- Owner/status/modified metadata
- Best-effort direct share counts
- Non-authoritative migration signals for migration or rebuild planning

See the tool documentation: [tools/solution-service-inspector/README.md](../tools/solution-service-inspector/README.md).

## Important interpretation note

The **Migration signals** tab is not an authoritative readiness assessment. It is a heuristic view derived from metadata the current user can read. Validate runtime usage, ownership, licensing, DLP policies, security access, connection ownership, and target-environment compatibility before making migration or rebuild decisions.
