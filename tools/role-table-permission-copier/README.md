# Role Table Permission Copier

## Purpose

The **Role Table Permission Copier** web resource helps admins manage table permissions in Dataverse security roles without fighting the standard role editor interface.

It is designed for scenarios like:

- Copying permissions from one table to many custom tables
- Selecting all user-created custom tables
- Filtering/searching by display name, schema name, or logical name
- Cloning a role and editing the cloned role
- Manually setting table permissions without selecting a source table

## File

Repository path:

[src\RoleTablePermissionCopier.html](src/RoleTablePermissionCopier.html)

Package paths:

[Unmanaged ZIP](../../packages/role-table-permission-copier/RoleTablePermissionCopierSolution.zip)

[Managed ZIP](../../packages/role-table-permission-copier/RoleTablePermissionCopierSolution_managed.zip)

## Screenshot

![Role Table Permission Copier screenshot](../../docs/assets/screenshots/role-table-permission-copier.png)

## Where to use it

Add this HTML file as a Dataverse **Webpage (HTML) web resource**, then add it to an admin model-driven app as a standalone page/navigation item.

The tool should run inside Dataverse so it can access:

- `Xrm.WebApi`
- The current Dataverse org URL
- The signed-in admin user's privileges

## Main workflow

1. Open the helper in the target environment.
2. Confirm the **Dataverse org URL** field is populated.
3. Click **Load roles**.
4. Search for and select a role.
5. Either:
   - Load the selected role, or
   - Clone the selected role first and load the clone.
6. Choose a permission source:
   - Use selected source table
   - Set permissions manually
7. Select target tables.
8. Click **Copy permissions**.

## Role loading

The tool loads roles from the current Dataverse environment. Once a role is selected, it loads:

- The role record
- Current role privileges
- Table metadata
- Privilege metadata

It uses the `roleprivilegescollection` / `roleprivileges` table to read role privileges, avoiding issues seen with the `RetrieveRolePrivilegesRole` function in some tenants.

## Clone role

The tool can clone an existing role:

1. Select a source role.
2. Enter a new role name.
3. Click **Clone role**.

The helper creates a new role in the same business unit and copies the source role's privileges to the new role. The cloned role is then loaded for editing.

## Permission source options

### Use selected source table

Select a table whose permissions should become the copy pattern. The preview shows the source table's permissions for:

- Create
- Read
- Write
- Delete
- Append
- Append To
- Assign
- Share

### Set permissions manually

Instead of selecting a source table, choose the depth for each permission directly:

- None
- User
- Business Unit
- Parent/Child BU
- Organization

This lets you apply a permission pattern even when no existing table has the exact settings you want.

## Target table selection

The target picker supports:

- Search by display name, logical name, or schema name
- Sort by display name, logical name, or schema name
- A to Z / Z to A sorting
- Select filtered results
- Clear selection
- Select all custom tables

## Custom table filtering

The helper defines "custom tables" as user/publisher-created tables, not Microsoft system or first-party app tables.

A table is treated as custom only when:

- Dataverse marks it as custom
- It has a publisher prefix like `abc_`
- It does not use blocked Microsoft/system prefixes

Blocked prefixes currently include:

```text
msdyn_
msdynce_
mspp_
msfp_
msft_
mspcat_
adx_
bot_
conversation_
dmsyn_
```

No-prefix out-of-the-box tables like `bot` or `activityfileattachment` are excluded from custom-table selection.

## Replace mode

When **Replace selected target table permissions to match source table** is enabled, the helper removes existing target-table permissions for the selected verbs before adding the new ones.

When disabled, it only removes/replaces permissions for verbs that are present in the source pattern.

## Required privileges

The signed-in user needs privileges to:

- Read roles
- Create roles, if cloning
- Read table metadata
- Read privilege metadata
- Read role privileges
- Add/remove privileges on roles

This tool does not bypass Dataverse security.

## Troubleshooting

| Symptom | Likely cause |
|---|---|
| Org URL is blank | Tool is not running inside a Dataverse app/web resource, or context is unavailable |
| Roles do not load | Current user lacks role read access, or URL points to the wrong org |
| Clone fails | User lacks role create/update privileges |
| Copy fails | User lacks permission to add/remove role privileges |
| Microsoft app tables appear in custom list | Add their publisher prefix to the blocked prefix list |
| Some table permissions are skipped | Target table does not expose the matching Dataverse privilege |

## Notes for GCC

The tool is compatible with GCC-style Dataverse org URLs such as:

`https://org.crm9.dynamics.com`

It should be hosted inside the same environment where the roles are being edited.

## Related tools

- [User Effective Security Roles](../user-effective-security-roles/README.md)
- [Team Role and People Manager](../team-role-people-manager/README.md)
- [Flow Dependency Viewer](../flow-dependency-viewer/README.md)
