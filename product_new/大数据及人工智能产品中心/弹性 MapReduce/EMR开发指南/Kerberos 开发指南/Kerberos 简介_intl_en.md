
From v2.1.0 on, EMR supports the creation of secure clusters, i.e., the open-source components in the cluster are launched in Kerberos secure mode. In this security environment, only authenticated clients can access the services (such as HDFS) of the cluster.

Below lists the components in EMR that currently supports Kerberos.

| Component Name | Version |
|---------|---------|
| Hadoop | 2.8.4 | 
| Hbase | 1.3.1 | 
| Hive | 2.3.3| 
| Hue | 4.4.0 | 
| Ooize | 4.3.1| 
| Presto | 0.7.1 | 
| Zookeeper | 3.4.9 | 

## Important Concepts
- **KDC**
Full name: Key distribution center
Role: Generating and managing tickets in the entire authentication process, including two services: AS and TGS.
- **AS**
Full name: Authentication service
Role: Generating TGTs for a client.
- **TGS**
Name: Ticket granting service
Role: Granting a client tickets for a specified service.
- **AD**
Name: Account database
Role: Storing the whitelist of all clients, and only clients in the whitelist can successfully apply for TGTs.
- **TGT**
Name: Ticket-granting ticket
Role: A ticket used to obtaining tickets.
- **client**
A client that wants to access a server.
- **server**
A server that provide a service for a certain business.

## Other Concepts
- **principal**
A subject of authentication, i.e., the username.
- **realm**
Realm is a little bit like a namespace in programming languages. In programming languages, a variable name only makes sense in a namespace. Similarly, a principal only makes sense in a realm. Generally, a realm can be seen as a "container" or "space" of a principal.
Correspondingly, the naming rule for principals is what_name_you_like@realm.
In Kerberos, it is customary to use uppercase letters to name a realm, such as EXAMPLE.COM.
- **password**
A password of a user, corresponding to a master_key in Kerberos. It can be stored in a keytab file; therefore, in all scenarios that require passwords in Kerberos, a keytab can be used as the input.
- **credential**
A credential is a proof that "proves that someone is truly of the claimed identity or that something can really happen". The specific meaning of the credential varies slightly by usage scenario:
 - For an individual principal, a credential is a password.
 - In the Kerberos authentication process, a credential means a variety of tickets.

## Authentication Process
During the process of accessing a server by a client, to ensure that both the client and the server are reliable, it is necessary to introduce a third-party authentication platform. Therefore, two services, AS and TGS, are designed. They are usually in the same service process and provided by a KDC for the implementation of MIT Kerberos.

The authentication process is divided into the following three steps:
1. A client requests access to a server from the Kerberos service. Kerberos first determines whether the client is trustworthy by checking whether it is in the blacklist and whitelist stored in the AD. After success, the AS returns a TGT to the client.
2. After receiving the TGT, the client continues to request access to the server from Kerberos. Kerberos uses the TGT in the message submitted by the client to determine that the client has the permissions, and then grants the server access ticket to the client.
3. After receiving the ticket, the client can access the server, but the ticket is only for the specified server. To access other servers, the client needs to apply to the TGS again.
![](https://main.qcloudimg.com/raw/0878d19a08a979608c84d1f4b759b683.png)
