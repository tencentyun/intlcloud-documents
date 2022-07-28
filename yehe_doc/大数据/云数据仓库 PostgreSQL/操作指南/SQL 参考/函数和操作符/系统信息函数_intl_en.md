The system information functions provided by the database can get session and system information as listed below:

| Function | Return Type | Description |
| -------------------------- | -------------------------- | -------------------------------------------- |
| current_database()         | name                       | Name of current database                             |
| current_schema()           | name                       | Name of current schema                             |
| current_schemas(boolean)   | name[]                     | Names of schemas in `search_path`               |
| current_user               | name                       | Username                                         |
| inet_client_addr()         | inet                       | Current client address (valid in remote connection mode)       |
| inet_client_port()         | int                        | Current client port (valid in remote connection mode)       |
| inet_server_addr()         | inet                       | IP address of the server that accepts connections (valid in remote connection mode) |
| inet_server_port()         | int                        | Port of the server that accepts connections (valid in remote connection mode)   |
| pg_postmaster_start_time() | timestamp   with time zone | Server start time                               |
| session_user               | name                       | Session username                                 |
| user                       | name                       | Equivalent to `current_user`                          |
| version()                  | text                       | PostgreSQL version                              |
