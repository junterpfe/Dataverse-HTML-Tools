Do you like Dataverse security roles, owner teams, and model-driven app security...

but hate the interface for actually managing all of it?

Same.

So I built a few small HTML web resources while testing out some ideas for making Dataverse security administration easier from inside a model-driven app.

These are not polished commercial products or official Microsoft tools. They are practical experiments that solved some pain points I kept running into.

If they are useful, feel free to modify them however you see fit. If you try them and think of changes, additions, or a better approach, I would genuinely like to hear it.

The first one is a User Effective Security Roles helper.

It gives admins one place to see the full access picture for a user:

- Direct security roles
- Team-inherited security roles
- Source teams
- Business units
- Clickable links back to Role and Team records
- Searchable and sortable results

It also supports actual assignment work:

- Add multiple direct roles
- Remove multiple direct roles
- Associate users with owner teams
- Remove owner-team memberships
- Copy role and team assignments from another user

The second one is a Role Table Permission Copier.

If you have ever edited table permissions in the standard Dataverse role editor, you know why this one matters.

This helper lets you:

- Load and search roles
- Clone an existing role and edit the clone
- Pick a source table permission pattern
- Or manually define Create, Read, Write, Delete, Append, Append To, Assign, and Share
- Search target tables
- Sort by display name, schema name, or logical name
- Select filtered tables
- Select all user-created custom tables
- Exclude Microsoft/system tables like msdyn_, msdynce_, mspp_, msfp_, adx_, and no-prefix OOTB tables
- Preview permissions before writing
- Copy the permission pattern across selected tables

The third one is a Team Role and People Manager.

This one focuses on Dataverse teams:

- Load a Team record directly from the Team form
- Add and remove team security roles
- Filter to custom roles only
- Add and remove people from owner teams
- Show current synced users for Entra-backed teams
- Link to Microsoft Entra for group membership management

That last part matters. For Entra security group teams and Microsoft 365 group teams, membership should be managed in Entra ID. The tool shows the synced Dataverse users read-only and links out to the group when the object ID is available.

The fourth one is a Flow Dependency Viewer.

This one focuses on solution cloud flows:

- Load a solution by name or ID
- See which flows depend on other flows
- See which flows depend on the current flow
- Calculate activation order
- Highlight external prerequisite flows
- List environment variables used by each flow
- Flag missing environment variable values in red
- Link directly to flows and edit missing environment variable values in-place

That matters when a solution has child flows, reusable flows, or environment-specific configuration. Before turning flows back on after an import, admins can see what needs to be activated first and which environment variables need values.

The biggest design choice: all of these tools run as Dataverse HTML web resources.

That means they use the current authenticated admin context and Xrm.WebApi. No separate service. No plugin. No desktop tool. No app registration just to do the admin work.

And they do not bypass security.

If the signed-in user cannot manage roles, teams, users, role privileges, solution components, flow state, or environment variables in Dataverse, the tools cannot either.

The real win is reducing friction in the repetitive security tasks admins run into all the time:

- What roles does this user really have?
- Which teams are giving this user access?
- Can I copy this user's assignments?
- Can I manage team roles without jumping around?
- Can I clone this role before changing it?
- Can I apply this table permission pattern to all my custom tables?
- Which cloud flows depend on other flows?
- Which environment variables are blocking flow activation?

Dataverse security is powerful, but the day-to-day admin UX can be click-heavy and hard to audit.

A little targeted tooling inside a model-driven app can make a big difference.

If you spend time managing security roles, teams, users, table permissions, or solution flow dependencies in Dataverse, this is the kind of admin experience I think we should be building more often.

Again, these are just me experimenting and sharing what I came up with. Take them, change them, improve them, or tell me what you would want added next.

#PowerPlatform #Dataverse #ModelDrivenApps #PowerApps #Dynamics365 #Microsoft365 #LowCode #AdminTools
