# Permission management

Permissions control who can perform actions in a workspace.
Every action requires explicit permission.

Users without permission cannot perform the action.

## Before you start

- You must have permission-management access (admin or equivalent).
- Confirm which workspace you are configuring.
- Identify which users need access and why.

## Permission model

Use this rule for all features:

- granted permission: action is available,
- missing permission: action is hidden, disabled, or blocked.

Apply this consistently to files, notebooks, environments, workspace settings, and member management.

## Grant permissions

1. Open the target workspace.
2. Go to members or permission settings.
3. Select a user.
4. Grant required permissions.
5. Save changes.

Grant only what is needed for current responsibilities.

## Revoke permissions

1. Open members or permission settings.
2. Select a user.
3. Remove unneeded permissions.
4. Save changes.

Revoke high-impact permissions immediately when no longer required.

## High-impact permissions

Treat these as restricted permissions:

- manage members and group settings,
- manage workspace settings,
- delete workspace.

These permissions should be assigned only to trusted users.

## Delete workspace permission

`Delete workspace` is destructive and irreversible.

Behavior requirements:
- only users with delete-workspace permission can execute deletion,
- other users cannot execute it,
- system must show a clear warning before confirmation.

Recommended warning text:

> This will permanently delete the workspace and all its data. This action cannot be undone.

## Role guidance (recommended)

Use role-based defaults, then fine-tune by permission:

- Viewer: read-only actions,
- Contributor: create/edit content actions,
- Admin: manage members/settings and high-impact actions.

## Validation checklist

- verify action visibility matches permissions,
- verify blocked actions show clear feedback,
- verify permission changes take effect immediately,
- verify workspace deletion is restricted to authorized users.

## Next steps

- Maintain a permission matrix by action and role.
- Add audit logging for grant/revoke/delete operations.
- Review high-impact permissions periodically.

#bioturing #biostudio #permission #workspace
