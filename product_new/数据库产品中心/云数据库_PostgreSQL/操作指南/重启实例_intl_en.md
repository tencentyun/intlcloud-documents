Restart is often necessary to maintain databases. Restarting a PostgreSQL instance is equivalent to restarting a database (service and process) on a local server.

## Restarting an Instance in the Console

1) Log in to the [TencentDB for PostgreSQL Console](https://console.cloud.tencent.com/pgsql).

2) Click **Restart** in the "Operation" column in the instance list to restart a running PostgreSQL instance.

## Precautions

1) Given the importance of databases to your business, please be cautious about restart. Before a restart, you are recommended to disconnect your database from the server and **stop data writes**.

2) Generally, it takes a dozen seconds to a few minutes for the restart to complete. The instance cannot provide any service during this process.

3) **There is a chance of failure in restarting a database**, which is **normal**. In this case, you can click **Restart** to try again.

4) Restarting an instance will not change any of its physical attributes, so the public and private IPs of the instance and any data stored in it will remain unchanged.

5) After the restart, reconnection to the database is required. Please make sure your business has a reconnection mechanism.

