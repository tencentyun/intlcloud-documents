TencentDB for TcaplusDB supports two table definition languages: Protocol Buffers (Protobuf) and Tencent Data Representation (TDR).
Protobuf is a method of serializing structured data developed by Google, which emphasizes simplicity and performance.
TDR is a platform-neutral data description language developed by Tencent, which combines the advantages of XML, binary language, and object-relational mapping (ORM) and is widely used in data serialization scenarios of Tencent's games.
Both languages are equally useful. Use either of them based on your usage habits.
This document describes how to define tables in TDR.

## Table Definition in TDR

TDR supports GENERIC tables and LIST tables. GENERIC tables represent the attributes of elements in the form of tables, such as students, employers, and game players. LIST tables are a list of records, such as game leaderboards and in-game emails (usually the last 100 emails).

You can create different types of tables in one XML file.

## Table Definition
- The `metalib` element is the root element of XML files.
- The `tagsetversion` attribute must be one.
- The `struct` element with the `primarykey` attribute needs to be defined as a table, or else it is just a structure.
- Each time the table structure is changed, the version attribute needs to be incremented by 1. The starting value of version attribute is always 1.
- The `primarykey` attribute is used to specify the primary key field. A GENERIC table supports up to four primary key fields and a LIST table supports up to three.
- The `splittablekey` attribute works as a shardkey to shard a TcaplusDB table into multiple shards and store them on multiple nodes. `splittablekey` must be one of the primary key fields. As a highly discrete `splittablekey` has better performance and a wide value range, we recommend a STRING `splittablekey`.
- The `desc` attribute describes the element.
- The `entry` element defines a field. Valid values: int32, string, char, int64, double, short.
- The `index` element defines an index which must contain `splittablekey`. Since the primary key can be used to query tables, the index should have a different attribute from the primary key.

## Sample Code for Table Description File in TDR

```
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
 
<metalib name="tcaplus_tb" tagsetversion="1" version="1">
 
  <!-- generic_table `users`, store the user' information -->
  <!-- an user may has many roles -->
  <struct name="users" version="1" primarykey="user_id,username,role_id" splittablekey="user_id" desc="user table">
    <entry name="user_id" type="uint64" desc="user id"/>
    <entry name="username" type="string" size="64" desc="login username"/>
    <entry name="role_id" type="int32" desc="a user can have multiple roles"/>
 
    <entry name="level" type="int32" defaultvalue="1" desc="role's level"/>
    <entry name="role_name" type="string" size="1024" desc="role's name"/>
    <entry name="last_login_time" type="string" size="64" defaultvalue="" desc="user login timestamp"/>
    <entry name="last_logout_time" type="string" size="64" defaultvalue="" desc="user logout timestamp"/>
 
    <index name="index1" column="user_id"/>
  </struct>
 
  <!-- list_table `mails`, store the role's mails -->
  <struct name="mails" version="1" primarykey="user_id,role_id" desc="mail table">
    <entry name="user_id" type="uint64" desc="user id"/>
    <entry name="role_id" type="int32" desc="a user may has many roles"/>
 
    <entry name="text" type="string" size="2048" desc="mail text"/>
    <entry name="send_time" type="string" size="64" defaultvalue="" desc="timestamp of the mail sent"/>
    <entry name="read_time" type="string" size="64" defaultvalue="" desc="timestamp of the mall read"/>
  </struct>
 
</metalib>
```
Additionally, you can use `union` to create nested type data.

The `union` element defines a simple type as a collection (union) of values from specified simple data types, such as INT and STRING. You can use `union` as a custom data type.
The `Macro` tag is used to define constants.

```
<macro name="DB_MAX_USER_MSG_LEN" value="301" desc="Max length of the message that user can define"/>
 <union name="DBPlayerMsg" version="1" desc="DB Player message">
   <entry name="SysMsgID"     type="uint8"         desc="Message ID" />
   <entry name="UsrMsg"       type="string"        size="DB_MAX_USER_MSG_LEN"   desc="player created message" />
 </union>
```