# Dataverse HTML Tools

Lightweight Dataverse and Power Platform admin tools built as HTML web resources for model-driven apps.

These tools run in the signed-in user's Dataverse context through `Xrm.WebApi`. They do not require a separate service, plug-in, desktop client, or app registration for the admin UI.

## Tools

| Tool | Source | Documentation |
|---|---|---|
| User Effective Security Roles | `tools\user-effective-security-roles\src\UserEffectiveSecurityRoles.html` | `tools\user-effective-security-roles\README.md` |
| Role Table Permission Copier | `tools\role-table-permission-copier\src\RoleTablePermissionCopier.html` | `tools\role-table-permission-copier\README.md` |
| Team Role and People Manager | `tools\team-role-people-manager\src\TeamRolePeopleManager.html` | `tools\team-role-people-manager\README.md` |
| Flow Dependency Viewer | `tools\flow-dependency-viewer\solution\src\WebResources\fdv_\flowdependencyviewer.htm` | `tools\flow-dependency-viewer\README.md` |

## Packages

| Tool | Unmanaged package | Managed package |
|---|---|---|
| User Effective Security Roles | `packages\user-effective-security-roles\UserEffectiveSecurityRolesSolution.zip` | `packages\user-effective-security-roles\UserEffectiveSecurityRolesSolution_managed.zip` |
| Role Table Permission Copier | `packages\role-table-permission-copier\RoleTablePermissionCopierSolution.zip` | `packages\role-table-permission-copier\RoleTablePermissionCopierSolution_managed.zip` |
| Team Role and People Manager | `packages\team-role-people-manager\TeamRolePeopleManagerSolution.zip` | `packages\team-role-people-manager\TeamRolePeopleManagerSolution_managed.zip` |
| Flow Dependency Viewer | `packages\flow-dependency-viewer\FlowDependencyViewerSolution.zip` | `packages\flow-dependency-viewer\FlowDependencyViewerSolution_managed.zip` |

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

Import the package ZIP for the tool from `packages`, or add the HTML file as a Dataverse **Webpage (HTML)** web resource, publish customizations, and place it in an admin model-driven app.

Use `themeOption=darkmode` when a model-driven app URL should force dark mode. The pages also handle that flag when it is encoded in the web resource `data` parameter.

## Security model

The tools do not bypass Dataverse or Power Platform security. All reads and writes run as the currently signed-in user. Restrict access with model-driven app access, web resource visibility, and Dataverse security roles.

See `SECURITY.md` for implementation notes and review guidance.

## Adding future tools

Add each new tool under `tools\<tool-slug>` with its own `README.md`, source files, and optional packaging project. Update this README and `docs\README.md` when adding a tool.
