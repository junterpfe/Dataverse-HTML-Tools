# Solution Service Inspector

## Purpose

The **Solution Service Inspector** web resource helps administrators inventory Power Platform assets and identify metadata-based migration or rebuild signals.

It is designed for scenarios like:

- Listing solutions in the current Dataverse environment
- Inspecting a selected solution's apps, flows, connection references, connectors, and environment variables
- Inspecting canvas apps, model-driven apps, and cloud flows that are not in a custom solution
- Extracting connected services and SharePoint URLs from readable Dataverse metadata
- Showing owner, status, modified date, direct-share counts, and heuristic migration signals
- Exporting inventory results to JSON or CSV

## Files

For the complete supported experience, install the [Dataverse HTML Tools Suite](../dataverse-html-tools-suite/README.md). Use this individual package only when deploying Solution Service Inspector without the Suite.

Repository paths:

[src\SolutionServiceInspector.html](src/SolutionServiceInspector.html)

[solution\src\WebResources\dht_\SolutionServiceInspector.html](solution/src/WebResources/dht_/SolutionServiceInspector.html)

[Unmanaged ZIP](../../packages/solution-service-inspector/SolutionServiceInspectorSolution.zip)

[Managed ZIP](../../packages/solution-service-inspector/SolutionServiceInspectorSolution_managed.zip)

The packaged solution contains the HTML web resource only.

## Where to use it

Use one of these deployment paths:

1. **Suite install:** import the [Dataverse HTML Tools Suite](../dataverse-html-tools-suite/README.md). This is the recommended option.
2. **Individual package:** build/import this managed or unmanaged solution ZIP, then add the imported `dht_\SolutionServiceInspector.html` web resource to an admin model-driven app as a standalone page/navigation item.
3. **Manual install:** add `src\SolutionServiceInspector.html` as a Dataverse **Webpage (HTML)** web resource, publish customizations, then add it to an admin model-driven app.

The tool runs in the signed-in user's Dataverse context. The no-app-registration version is **same-environment only**: to inspect a different environment, open or deploy the web resource in that target environment.

## Main features

### Inventory modes

The **Inspect** selector supports:

| Mode | What it scans |
|---|---|
| Solution | Starts from `solutioncomponents`, then reads referenced app, flow, connector, connection reference, and environment variable records |
| App or cloud flow | Lists environment-level canvas apps, model-driven apps, and cloud flows directly so assets outside a custom solution can be inspected |

### Inventory table

The inventory view shows:

- Asset name and type
- Owner when readable from Dataverse lookup annotations
- Status/lifecycle value when exposed by Dataverse
- Last modified date
- Best-effort direct user/team share counts
- Heuristic risk signals

### Service and URL detection

The inspector parses readable JSON/XML/text metadata for:

- Connection reference connector IDs
- SharePoint site URLs across Commercial, GCC, GCC High, and DoD hostnames
- Non-platform external dependency URLs
- Custom connector and HTTP endpoint indicators

Power Platform launch URLs, Dataverse self-links, auth endpoints, and platform CDN URLs are filtered out so they are not treated as app dependencies.

### Migration signals

The **Migration signals** tab is intentionally non-authoritative. It highlights heuristic signals from readable metadata, including:

- Standalone assets not currently inspected through a custom solution
- SharePoint URL dependencies
- Likely hard-coded URLs
- Non-platform external URL dependencies
- HTTP/custom endpoint usage
- Custom connectors
- Broad or team-based direct sharing
- Unknown direct-share counts
- Inactive or stale assets
- Missing visible owner data

These signals are prompts for review, not a migration readiness score.

## Light and dark mode

The page defaults to light mode, matching the other HTML tools. To enable dark mode, include:

```text
themeOption=darkmode
```

This also works when the value is encoded inside the model-driven app web resource `data` parameter.
Dataverse `themeOption=darkmode` signals are detected in the web resource URL, encoded URL values, and accessible parent host URLs.

## Required privileges

The current user needs Dataverse privileges to read:

- Solutions and solution components
- Cloud flows from the `workflow` table
- Canvas apps from the `canvasapp` table
- Model-driven apps from the `appmodule` table
- Connection references
- Connectors
- Environment variable definitions and values
- Principal object access rows, if direct-share counts should be shown

The tool does not bypass Dataverse, Power Platform, or tenant security.

## Limitations

- The no-app-registration version is same-environment only.
- Migration signals are heuristic and based only on metadata readable by the current user.
- Direct share counts are best-effort from Dataverse `PrincipalObjectAccess`; group membership, security role access, and some canvas app run-only sharing may require Power Platform Admin APIs or PowerShell.
- Runtime usage, flow run history, licensing detail, DLP policy impact, and business criticality are not fully determined by this page.
- Dynamic URLs composed at runtime may not be detected.

## Troubleshooting

| Symptom | Likely cause |
|---|---|
| Cross-environment URL returns 401 | Browser session credentials are scoped to the environment hosting the web resource |
| Share counts show Unknown | Current user lacks access to principal object access data, or the table is unavailable in that context |
| No apps or flows are listed | Current user lacks read access, or the environment stores the target asset type in APIs not exposed to this web resource |
| Platform URLs appear as dependencies | Confirm the page shows the latest build and re-publish the web resource |
| Page opens in dark mode unexpectedly | Remove `themeOption=darkmode` from the web resource or parent host URL |

## Related tools

- [Flow Dependency Viewer](../flow-dependency-viewer/README.md)
- [User Effective Security Roles](../user-effective-security-roles/README.md)
- [Role Table Permission Copier](../role-table-permission-copier/README.md)
- [Team Role and People Manager](../team-role-people-manager/README.md)
