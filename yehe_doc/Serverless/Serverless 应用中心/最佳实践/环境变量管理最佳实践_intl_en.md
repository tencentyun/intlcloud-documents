## Using serverless-global Component for Global Variable Management

You may encounter some global variables when using Serverless Components; for example, you may need to configure the same information such as database for multiple functions. You can use the serverless-global component to reuse and manage such variables as follows:

Add the global configuration field in `Yaml` first and then directly refer to it in the corresponding component by means of `${Conf.mysql_host}`.
```yaml
Conf:
  component: "serverless-global"
  inputs:
    mysql_host: gz-cdb-mytest.sql.tencentcdb.com
    mysql_user: mytest
    mysql_password: mytest
    mysql_port: 62580
    mysql_db: mytest
    mini_program_app_id: mytest
    mini_program_app_secret: mytest


Album_Login:
  component: "@serverless/tencent-scf"
  inputs:
    name: Album_Login
    codeUri: ./album/login
    handler: index.main_handler
    runtime: Python3.6
    region: ap-shanghai
    environment:
      variables:
        mysql_host: ${Conf.mysql_host}
        mysql_port: ${Conf.mysql_port}
        mysql_user: ${Conf.mysql_user}
        mysql_password: ${Conf.mysql_password}
        mysql_db: ${Conf.mysql_db}
```
