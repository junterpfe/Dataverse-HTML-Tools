# Team Role and People Manager

## Purpose

The **Team Role and People Manager** web resource gives administrators a cleaner way to manage Dataverse team security roles and team membership from a Team form.

It is designed for scenarios like:

- Seeing which security roles are assigned to a team
- Adding or removing team roles
- Adding or removing people from owner teams
- Viewing current users on Entra-backed teams
- Linking directly to the Entra group for membership management

## File

Repository path:

`src\TeamRolePeopleManager.html`

Package paths:

`..\..\packages\team-role-people-manager\TeamRolePeopleManagerSolution.zip`

`..\..\packages\team-role-people-manager\TeamRolePeopleManagerSolution_managed.zip`

## Where to use it

Add this HTML file as a Dataverse **Webpage (HTML) web resource**, then place it on the **Team (`team`) form** in a model-driven app.

When adding the web resource to the form, enable:

**Pass record object-type code and unique identifier as parameters**

The web resource uses the current Team record ID to load and manage that team's roles and people.

You can also use it standalone by pasting a Team record URL or team GUID into the page.

## Main features

### Team summary

The tool shows:

- Loaded team name
- Team type
- Security role count
- People count

### Team role management

Admins can add or remove one or more security roles from the team using searchable multi-select controls.

The tool uses Dataverse Web API `Associate` and `Disassociate` operations with:

- `teamroles_association`
- `team`
- `role`

### Custom role filter

The role pickers include a **Show custom roles only** checkbox.

When enabled, the add/remove role lists only show roles that are:

- Not managed
- Not system-generated

This helps admins focus on custom/admin-created security roles instead of first-party or system-generated roles.

### Owner team people management

For owner teams, admins can:

- Search users by name, email, or domain name
- Add people to the team
- Remove existing team members

The tool uses:

- `teammembership_association`
- `team`
- `systemuser`

### Entra-backed team handling

For Microsoft Entra-backed teams, including security group teams and Microsoft 365 group teams, the tool switches the people section to read-only mode.

When the team is Entra-backed:

- Add people controls are hidden
- Remove people controls are hidden
- Current synced Dataverse users are shown read-only
- A link appears to edit group membership in Microsoft Entra when the Entra group object ID is available

This is intentional because group membership should be managed in Entra ID, not directly in Dataverse team membership.

### Commercial, GCC, GCCH, and DoD links

The tool builds the Entra group edit link based on the detected cloud.

- Commercial and GCC use `https://entra.microsoft.com`
- GCCH/DoD-style URLs use `https://entra.microsoft.us`

If your tenant uses a different portal URL pattern, update the `getEntraPortalBaseUrl` function in the HTML.

### Light and dark mode

The tool supports light/dark display and checks the model-driven app URL, parent URL, top URL, and referrer for the dark-mode flag.

It also includes a manual Light/Dark selector.

## Required privileges

The current user needs Dataverse privileges to:

- Read teams
- Read users
- Read security roles
- Read team membership
- Read team role associations
- Add/remove team roles
- Add/remove owner-team members

For Entra-backed teams, the current user also needs the appropriate Entra permissions outside Dataverse to edit group membership in the Entra portal.

## Limitations

- Does not directly manage Entra group membership.
- Does not force/sync missing Entra members into Dataverse.
- Does not bypass Dataverse security.
- People add/remove is only available for owner teams.
- Entra group team users shown in Dataverse are only users already synced/provisioned into the environment.

## Troubleshooting

| Symptom | Likely cause |
|---|---|
| Page cannot find the team | Web resource was not configured to pass record ID parameters |
| Add/remove people controls are hidden | Team is Entra-backed or not an owner team |
| Entra link is missing | Team does not expose an `azureactivedirectoryobjectid` value |
| Current users list is missing expected Entra members | Users may not be synced/provisioned into the Dataverse environment |
| Add/remove roles fails | Current user lacks privileges to manage team roles |
| Add/remove people fails | Current user lacks privileges to manage owner-team membership |

## Related tools

- [User Effective Security Roles](UserEffectiveSecurityRoles.md)
- [Role Table Permission Copier](RoleTablePermissionCopier.md)
- [Flow Dependency Viewer](FlowDependencyViewer.md)
