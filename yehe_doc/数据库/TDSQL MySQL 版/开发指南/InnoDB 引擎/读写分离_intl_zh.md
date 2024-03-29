
TDSQL MySQL版 实例支持下列几种模式的读写分离：
- 通过增加 slave 注释标记，即在 SQL 中添加 /`*slave*/` 这样的标记，并且 mysql 后面增加 -c 参数来解析注释 `mysql -c -e "/*slave*/sql"`，该 SQL 会发送给备机。
>?支持` /*slave:slaveonly*/`、` /*slave:20*/`、` /*slave:slaveonly,20*/`这几种形式，数值表示 slave 应该满足的延迟，slaveonly 表示在没有符合条件的 slave 时，不会将查询发送给主节点。
>
```
//主机读//
select * from emp order by sal，deptno desc；
//从机读//
/*slave*/ select * from emp order by sal，deptno desc；
```
- 由只读帐号发送的请求会根据配置的属性发给备机。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Bpmr055_10.png)
