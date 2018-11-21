## Role Overview

Roles are used in Snova to manage the access permissions to the database. The concept of role usually includes two parts: users and groups. A role can be a general user of the database (i.e. user) or a user group (i.e. group). A role can own database objects (such as tables and views) and can assign access permissions to those objects to other roles.

When creating a cluster, you are prompted to set the initial username and password of the initial user that is the "admin user" and has the permissions to create users, create databases and log in. After the cluster is created, you can use the "admin user" to connect to databases. Generally, the admin user has the maximum permissions, which means that this account should be used by as few people as possible. You can use the admin user to create other users and grant them the required permissions. For more information, see [User Group](https://cloud.tencent.com/document/product/878/20072#.E7.94.A8.E6.88.B7.E7.BB.84) and [Object Permission Management](https://cloud.tencent.com/document/product/878/20072#.E5.AF.B9.E8.B1.A1.E6.9D.83.E9.99.90.E7.AE.A1.E7.90.86). You can also create databases and other objects. For more information, see [Define a Database](https://cloud.tencent.com/document/product/878/20070). To learn how to log in to a database, see [Connecting to a Database](https://cloud.tencent.com/document/product/878/20064#.E4.BA.8C.-.E8.BF.9E.E6.8E.A5.E6.95.B0.E6.8D.AE.E5.BA.93).

## Creating a User

Roles are divided into users (for users) and groups (for user groups). Usually, a role at the user level (hereinafter referred to as user) has the permissions to log in to Snova databases and initialize sessions. Therefore, when creating a user, you must grant it the LOGIN permission. For example:

```
CREATE role jsmith with LOGIN
```

Through the step above, a user with the LOGIN permission who can connect to a database is created. In addition to the LOGIN permission, Snova's access management has the following additional permissions for users. You can grant the desired permissions when creating a role using the CREATE ROLE statement.

| Permission value | Purpose | Default value |
| ---------------------------------- | -------------------------------------------------------- | ---------------- |
| SUPERUSER 	&Iota; NOSUPERUSER           | Super user permissions; only a superuser can create other superusers         | NOSUPERUSER      |
| CREATEDB &Iota; NOCREATEDB             | Permission to create databases                                         | NOCREATEDB       |
| CREATEROLE &Iota; NOCREATEROLE         | Create and manage roles                                           | NOCREATEROLE     |
| INHERIT &Iota; NOINHERIT               | Determine that the user inherits the permissions of the group                            | INHERIT          |
| LOGIN &Iota; NOLOGIN                   | Permission to log in to databases; general users have this permission, while groups don't | NOLOGIN          |
| CONNECTION LIMIT                   | Limit the number of concurrent connections to a database; -1 means unlimited            | -1               |
| CREATEEXTTABLE &Iota; NOCREATEEXTTABLE | Permission to create external tables                                           | NOCREATEEXTTABLE |
| PASSWORD                           | Set a password when creating a user                                       | Nil               |
| VALID UNTIL 'timestamp'            | Password expiration time                                           | Nil              |
| RESOURCE QUEUE 'name'              | The resource queue name to which the created query is scheduled after the user is connected               | pg_default       |

In addition to granting permissions to users when creating them, you can also use the ALTER ROLE statement to reassign permissions after the users are created. For example:

```
ALTER role jsmith with CREATEROLE;
```

### Group

A group (i.e. user group) is a special role that does not have the LOGIN permission. The group is usually set to a combination of permissions that are often used together, and the permissions can be granted to or revoked from users as a whole.

You can create a role (i.e. a group) that is granted a combination of permissions by using the following statement.

```
Create role, Create DB, Cannot login
```

You can also easily create or cancel affiliation of other users with this group using the GRANT TO or REVOKE FROM statements. Users belong to the user group inherit permissions from this group.

- GRANT TO statement example: ![](https://main.qcloudimg.com/raw/edd92eff662907accd1c0ddf0ea60f32.png) This makes the user "jsmith" belong to the group "manager".
- REVOKE FROM statement example: ![](https://main.qcloudimg.com/raw/d6f48b8d66ba357b761052a2cdfbe90a.png) This cancels the affiliation of the user "jsmith" with the group "manager".

## Object Permission Management

When an object (such as a database, table, schema or function) is created, there must be an owner that is typically the user who executes the object creation statement. Initially, only the owner has all the operational permissions of this object. For example:

```
GRANT INSERT ON test TO  jsmith;
```

You can grant the INSERT permission of "test" to the user "jsmith" using the statement above, which can also be canceled using REVOKE FROM.

Similarly, all the objects belonging to a user can be transferred to another user using the REASSIGN OWNED statement, for example:

```
SET ROLE jsmith;   // Switch to user "jsmith"
CREATE TABLE jsmithtest (age int, id int); // Create a new table
SET ROLE gpadmincloud;        // Switch back to the superuser
reassign owned by jsmith to lambuser;   // Transfer all the objects belonging to "jsmith" to "lambuser"
```

> Since objects belonging to a superuser cannot be transferred to another user as system objects belong to the super object, we need to create a table with non-superusers.

![](https://main.qcloudimg.com/raw/b9164fd90cc589e7a5c0a5d4d28f6816.png)

This transfers the objects from "jsmith" to "lambuser".
