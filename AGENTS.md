# Snowflake Cortex Code Project Instructions

## Project purpose

This repository is a development workspace for working with Snowflake through
Cortex Code / CoCo Desktop.

SQL scripts and other project assets should be stored in Git and reviewed before
being executed against Snowflake.

## Default Snowflake development environment

Unless explicitly instructed otherwise, use:

- Role: `COCO_LAB_ROLE`
- Warehouse: `COCO_LAB_WH`
- Database: `COCO_LAB_DB`
- Schema: `DEV`

Prefer fully qualified Snowflake object names:

`COCO_LAB_DB.DEV.<OBJECT_NAME>`

## Snowflake safety rules

1. Never use `ACCOUNTADMIN`, `ORGADMIN`, `SECURITYADMIN`, `USERADMIN`,
   or `SYSADMIN` unless the user explicitly requests it in the current conversation.

2. Do not create, alter, or delete objects outside `COCO_LAB_DB.DEV`
   unless the user explicitly authorizes another target environment.

3. Never change account-level configuration, users, roles, grants,
   authentication settings, network policies, or Cortex account parameters
   without explicit user instruction.

4. Before executing DDL or DML:
   - show what will be changed;
   - identify the target database, schema, and object;
   - use the configured development role;
   - wait for approval when the operation is potentially destructive.

5. Treat the following as destructive operations and require explicit approval:
   - `DROP`
   - `TRUNCATE`
   - destructive `DELETE`
   - destructive `UPDATE`
   - replacing existing production objects
   - privilege or ownership changes

6. Prefer read-only inspection before modifying existing Snowflake objects.

7. After making a Snowflake change, run an appropriate verification query.

## SQL development

- Store reusable SQL in the `sql/` directory.
- Use clear and descriptive file names.
- Prefer explicit database and schema references.
- Keep SQL readable and structured.
- Add comments where the purpose of a script is not obvious.
- Do not hard-code credentials, passwords, tokens, private keys, or secrets.
- Do not put sensitive production data into repository files.

## Git workflow

Before committing:

1. Run `git status`.
2. Review the relevant `git diff`.
3. Confirm that only intended files are staged.
4. Use a concise descriptive commit message.

Never:

- force push;
- run `git reset --hard`;
- run `git clean -fd`;
- amend an existing commit;
- rewrite Git history;

unless the user explicitly requests the operation.

Do not use `git add .` when only specific files should be committed.
Stage the intended files explicitly.

## GitHub

The default remote is:

`origin`

The default branch is:

`main`

Do not push changes until the user has reviewed the intended changes or
explicitly requested the push.

## Working approach

For non-trivial tasks:

1. Inspect the existing project and Snowflake context.
2. Explain the proposed approach.
3. Create or modify the project files.
4. Show the relevant changes.
5. Execute against Snowflake only when appropriate.
6. Verify the result.
7. Review Git changes.
8. Commit and push only when requested.

When there is uncertainty about the target Snowflake environment, stop and ask
rather than guessing.
