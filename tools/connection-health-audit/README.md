# Connection Health Audit

The Connection Health Audit page starts a background Power Automate collector and displays connection status, authentication errors, and basic redundancy signals without requiring a download/upload step.

## Features

- Load a dropdown of environments accessible to the configured Power Apps for Makers connection.
- Create an audit request for the selected environment.
- Poll the Dataverse audit row until the collector completes.
- Display connection name, connector/API ID, owner, status, and error message.
- Use the Connections, Issues, and Duplicate groups summary cards as clickable filters.
- Highlight connections that share a connector with other connections.
- Load previous completed audit runs for an environment without starting a new flow run.
- Analyze connection references grouped by connector, bound connection, visible solution membership, and detected usage.
- Review same-connector references that use the same or different accounts/connections as consolidation candidates.
- Start with same-connector consolidation candidates, switch to the full reference inventory when needed, and export the visible analysis to CSV.
- Detect likely flow, canvas app, and model-driven app usage by searching readable component metadata for the reference logical name.
- Compare bound connection IDs and, when a health audit exists for the same hosted environment, map IDs to reported account identities.
- Store the raw result JSON and summary counts in the `dht_ConnectionAudit` table.
- Run from the `Admin Tools` app through the Dataverse HTML Tools Suite.

## Requirements

The Suite includes the `Connection Health Audit Collector` flow and the `dht_ConnectionAudit` table. After import, configure these flow connection references: **Connection Health Audit - Dataverse** and **Connection Health Audit - Power Apps for Makers**. The Makers connection discovers accessible environments and lists connections in the selected environment. Until those references are configured, environment discovery and audit rows remain in `Requested` status.

The connection status is reported by the Power Platform connector. A status such as `Error` or an `Unauthorized` error is an authentication or configuration signal, not a test that exposes credentials or tokens.

## Limitations

- The first version audits the environment selected in the page and stores one JSON result per request.
- Connection references and solution/app usage are still read by the Solution Service Inspector; this page reports connection-instance health.
- Redundancy grouping is calculated in the page by connector ID, so multiple connections using the same connector are highlighted; flow records returned by the connector are excluded from connection counts.
- The reference analysis is solution-aware. Same-connector references are grouped for review, with stronger candidates when they share a bound connection and caution when they use different accounts or connections.
- Connection-reference records do not directly expose the bound connection account. Account mapping is best-effort from a completed same-environment health audit, so confirm ownership before replacing references.
- Usage detection is best-effort and can only scan assets and metadata visible to the current Dataverse user. It does not prove that an unlisted reference is unused.
- Account identity mapping requires a completed connection-health audit for the same environment hosting this page. Cross-environment account identity is not inferred.
- No secrets, access tokens, or connection credentials are stored.
