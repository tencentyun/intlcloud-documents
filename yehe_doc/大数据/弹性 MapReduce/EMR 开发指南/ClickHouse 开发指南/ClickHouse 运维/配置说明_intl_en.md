The ClickHouse server configuration files are located in `/etc/clickhouse-server` and include `config.xml`, `metrika.xml`, and `users.xml`, among which `config.xml` is the primary configuration file of the ClickHouse server.

## config.xml
 
Under the `conf.d` and `config.d` folders at the same level as the `config.xml` configuration file, you can create an `*.xml` file to override the configurations in the `config.xml` file (**however, you are not recommended to do so; instead, you are recommended to centrally distribute configurations by using the configuration delivery feature in the console**).

For example, create a `config.d` directory at the same level as the `config.xml` file:
1. Modify the TCP port listened on by the `clickhouse-server`, which is port 9000 in the `config.xml` file by default. Create a `tcp_port.xml` file in the `config.d` folder and add the following content to it:
```
<yandex>
       <tcp_port>9900</tcp_port>
</yandex>
```
Restart the `clickhouse-server` and you can find that the TCP port listened on has been changed to 9000.
2. Add the `metric_log` configuration. Create a `metric_log.xml` file and add the following content to it:
```
<yandex>
       <metric_log>
           <database>system</database>
           <table>metric_log</table>
           <flush_interval_milliseconds>7500</flush_interval_milliseconds>
           <collect_interval_milliseconds>1000</collect_interval_milliseconds>
       </metric_log>
</yandex>
```
Restart the `clickhouse-server` and `clickhouse-client` and run `SELECT * FROM system.metric_log LIMIT 1 FORMAT Vertical;` to create the `system.metric_log` table automatically.

## metrika.xml

ClickHouse configurations can be "replaced". You can use the **incl** attribute to replace configurations in `config.xml` with those in the specified file, so that the primary configuration file will not become too redundant or hard to maintain. In the default `config.xml` configuration file, you can see that the three tags `<remote_servers>`, `<macros>`, and `<zookeeper>` all have the **incl** attribute. Therefore, you can load the corresponding `<clickhouse_remote_servers>`, `<macros>`, and `<zookeeper-servers>` configuration items in the `metrika.xml` file into the `config.xml` file. The path of the file for replacement is `/etc/metrika.xml` by default and can be modified through the `<include_from>` configuration item.

>If the configuration items to be replaced in the `incl` attribute do not exist, the event will be recorded in a log. If you do not want to log such events, you can use the `optional="true"` attribute.

## users.xml

In the `config.xml` configuration file, `users_config` indicates the path of the user-related configuration file, which is `users.xml` by default. In `users.xml`, you can configure information such as user password, permission, profile, and quota. Different users can have different configurations.

You can create a `users.d` directory in the `user.xml` statistics directory and add user-related configurations (e.g., `/etc/clickhouse-server/users.d/testUser.xml`) under it so as to reduce redundancy of the `users.xml` file and simplify the maintenance.
```
<yandex>
    <users>
      <testUser>
          <profile>default</profile>
            <networks>
                  <ip>::/0</ip>
            </networks>
          <password>12345</password>
          <quota>default</quota>
      </testUser>
    </users>
</yandex>
```
For the specific server parameter configurations and settings, please see [Server Settings](https://clickhouse.tech/docs/en/operations/server-configuration-parameters/settings/) and [Settings](https://clickhouse.tech/docs/en/operations/settings/) on the official website.



