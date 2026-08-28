# Dataverse HTML Tools

Lightweight Dataverse and Power Platform admin tools built as HTML web resources for model-driven apps.

These tools run in the signed-in user's Dataverse context through `Xrm.WebApi`. They do not require a separate service, plug-in, desktop client, or app registration for the admin UI.

## Tools

| Tool | Source | Documentation |
|---|---|---|
| [User Effective Security Roles](tools/user-effective-security-roles/README.md) | [HTML](tools/user-effective-security-roles/src/UserEffectiveSecurityRoles.html) | [Docs](tools/user-effective-security-roles/README.md) |
| [Role Table Permission Copier](tools/role-table-permission-copier/README.md) | [HTML](tools/role-table-permission-copier/src/RoleTablePermissionCopier.html) | [Docs](tools/role-table-permission-copier/README.md) |
| [Team Role and People Manager](tools/team-role-people-manager/README.md) | [HTML](tools/team-role-people-manager/src/TeamRolePeopleManager.html) | [Docs](tools/team-role-people-manager/README.md) |
| [Flow Dependency Viewer](tools/flow-dependency-viewer/README.md) | [HTML web resource](tools/flow-dependency-viewer/solution/src/WebResources/fdv_/flowdependencyviewer.htm) | [Docs](tools/flow-dependency-viewer/README.md) |
| [Solution Service Inspector](tools/solution-service-inspector/README.md) | [HTML](tools/solution-service-inspector/src/SolutionServiceInspector.html) | [Docs](tools/solution-service-inspector/README.md) |

## Screenshots

Screenshots use sanitized sample data.

| User Effective Security Roles | Role Table Permission Copier |
|---|---|
| ![User Effective Security Roles screenshot](docs/assets/screenshots/user-effective-security-roles.png) | ![Role Table Permission Copier screenshot](docs/assets/screenshots/role-table-permission-copier.png) |

| Team Role and People Manager | Flow Dependency Viewer |
|---|---|
| ![Team Role and People Manager screenshot](docs/assets/screenshots/team-role-people-manager.png) | ![Flow Dependency Viewer screenshot](docs/assets/screenshots/flow-dependency-viewer.png) |

## Packages

| Tool | Unmanaged package | Managed package |
|---|---|---|
| User Effective Security Roles | [Unmanaged ZIP](packages/user-effective-security-roles/UserEffectiveSecurityRolesSolution.zip) | [Managed ZIP](packages/user-effective-security-roles/UserEffectiveSecurityRolesSolution_managed.zip) |
| Role Table Permission Copier | [Unmanaged ZIP](packages/role-table-permission-copier/RoleTablePermissionCopierSolution.zip) | [Managed ZIP](packages/role-table-permission-copier/RoleTablePermissionCopierSolution_managed.zip) |
| Team Role and People Manager | [Unmanaged ZIP](packages/team-role-people-manager/TeamRolePeopleManagerSolution.zip) | [Managed ZIP](packages/team-role-people-manager/TeamRolePeopleManagerSolution_managed.zip) |
| Flow Dependency Viewer | [Unmanaged ZIP](packages/flow-dependency-viewer/FlowDependencyViewerSolution.zip) | [Managed ZIP](packages/flow-dependency-viewer/FlowDependencyViewerSolution_managed.zip) |
| Solution Service Inspector | [Unmanaged ZIP](packages/solution-service-inspector/SolutionServiceInspectorSolution.zip) | [Managed ZIP](packages/solution-service-inspector/SolutionServiceInspectorSolution_managed.zip) |

## Repository layout

```text
Dataverse-HTML-Tools\
  docs\                         Suite-level docs, article drafts, and shared assets
  packages\                     Importable solution ZIPs when a tool needs packaging
  tools\
    <tool-slug>\
      README.md                 Tool-specific documentation
      src\                      Standalone HTML web resources
      solution\                 Dataverse solution packaging source
```

## Deployment

Use one of these deployment paths:

1. **Packaged install:** import the tool's managed or unmanaged ZIP from [`packages`](packages), publish customizations if prompted, then add the imported web resource to an admin model-driven app.
2. **Manual install:** add the tool's HTML file as a Dataverse **Webpage (HTML)** web resource, publish customizations, then add that web resource to an admin model-driven app.

Use `themeOption=darkmode` when a model-driven app URL should force dark mode. The pages also handle that flag when it is encoded in the web resource `data` parameter. Dataverse/Power Platform HTML tools should default to light mode unless that explicit dark-mode flag is present.

## Security model

The tools do not bypass Dataverse or Power Platform security. All reads and writes run as the currently signed-in user. Restrict access with model-driven app access, web resource visibility, and Dataverse security roles.

See [SECURITY.md](SECURITY.md) for implementation notes and review guidance.

## Adding future tools

Add each new tool under `tools\<tool-slug>` with its own `README.md`, source files, and optional packaging project. Update this README and [`docs\README.md`](docs/README.md) when adding a tool.
