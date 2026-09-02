# Dataverse HTML Tools Suite

`Dataverse HTML Tools Suite` is the combined installation option for all repository tools. It includes the `Admin Tools` model-driven app, existing HTML web resources, and dedicated User and Team forms.

## Included experience

- `Admin Tools` model-driven app.
- Default User and Team list views.
- `Admin Tools User` form, preserving standard tabs and adding `Effective Security Roles` and `User Record Access`.
- `Admin Tools Team` form, preserving standard tabs and adding `Team Role and People Manager`.
- Standalone navigation pages for Flow Dependency Viewer, Role Table Permission Copier, and Solution Service Inspector.

The included User tool supports direct-role, owner-team, and optional record-specific access-team copying with `Add` and `Clone` modes. The User and Team tools identify group-backed Dataverse teams and link available Entra group IDs to the correct Commercial, GCC, GCC High, or DoD Entra admin center.

## Install

Import one archive from [`packages/dataverse-html-tools-suite`](../../packages/dataverse-html-tools-suite):

- `DataverseHTMLToolsSuite_managed.zip` for a managed deployment.
- `DataverseHTMLToolsSuite.zip` for development or customization.

After import, publish customizations if Dataverse prompts for it, then grant users access to the `Admin Tools` app and required Dataverse privileges. The tools execute using the signed-in user's permissions.

## Build

Build `solution/DataverseHTMLToolsSuite.cdsproj` in Release configuration. It produces both managed and unmanaged solution ZIPs.