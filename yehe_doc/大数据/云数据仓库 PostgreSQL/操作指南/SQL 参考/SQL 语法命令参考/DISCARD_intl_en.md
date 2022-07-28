It discards the session state.

## Synopsis
```sql
DISCARD { ALL | PLANS | TEMPORARY | TEMP }
```

## Description
`DISCARD` releases internal resources associated with a database session. These resources are normally released at the end of the session.
`DISCARD TEMP` drops all temporary tables created in the current session.
`DISCARD PLANS` releases all internally cached query plans.
`DISCARD ALL` resets a session to its original state, discarding temporary resources and resetting session-local configuration changes.

## Parameters
TEMPORARY, TEMP
Drops all temporary tables created in the current session.

PLANS
Releases all cached query plans.

ALL
Releases all temporary resources associated with the current session and resets the session to its initial state. Currently, this has the same effect as executing the following sequence of statements:

```sql
SET SESSION AUTHORIZATION DEFAULT;
RESET ALL;
DEALLOCATE ALL;
CLOSE ALL;
UNLISTEN *;
SELECT pg_advisory_unlock_all();
DISCARD PLANS;
DISCARD TEMP;
```

## Notes
`DISCARD ALL` cannot be executed inside a transaction block.

## Compatibility
`DISCARD` is a database extension.
