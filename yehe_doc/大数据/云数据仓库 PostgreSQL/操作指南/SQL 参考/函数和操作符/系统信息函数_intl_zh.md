数据库提供的系统信息函数可以获取会话和系统信息，具体见下面表格。

| 函数名                     | 返回值                     | 说明                                         |
| -------------------------- | -------------------------- | -------------------------------------------- |
| current_database()         | name                       | 现在的数据库名称                             |
| current_schema()           | name                       | 现在的 schema 名称                             |
| current_schemas(boolean)   | name[]                     | search_path 设置的所有 schema               |
| current_user               | name                       | 用户                                         |
| inet_client_addr()         | inet                       | 当前客户端的地址（远程连接模式下有效）       |
| inet_client_port()         | int                        | 当前客户端的端口（远程连接模式下有效）       |
| inet_server_addr()         | inet                       | 接受连接的服务端 IP 地址（远程连接模式下有效） |
| inet_server_port()         | int                        | 接受连接的服务端端口（远程连接模式下有效）   |
| pg_postmaster_start_time() | timestamp   with time zone | 服务器启动时间                               |
| session_user               | name                       | 会话用户名称                                 |
| user                       | name                       | 等价于 current_user                          |
| version()                  | text                       | PostgreSQL 版本                              |
