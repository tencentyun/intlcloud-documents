This document uses MIT's Kerberos as the KDC service and assumes that KDC has been properly installed and started. To use Kerberos, create a realm, add the principals of relevant roles (including server and client), and generate a keytab file.

## Creating a Database
Run the `kdb5_util` command to create a database for storing information about the principals.
```
kdb5_util -r EXAMPLE.COM create -s
Initializing database '/var/krb5/principal' for realm 'EXAMPLE.COM'
master key name 'K/M@EXAMPLE.COM'
You will be prompted for the database Master Password.
It is important that you NOT FORGET this password.
Enter KDC database master key: <Type the key>
Re-enter KDC database master key to verify: <Type it again>
```

## Adding a Principal
```
 kadmin.local
 kadmin.local: add_principal -pw testpassword test/host@EXAMPLE.COM

 WARNING: no policy specified fortest/host@EXAMPLE.COM; defaulting to no policy
 Principal "test/host@EXAMPLE.COM" created.
```

## Generating a Keytab File
```
 kadmin.local
 kadmin.local: ktadd -k /var/krb5kdc/test.keytab test/host@EXAMPLE.COM

 Entry for principal test/host@EXAMPLE.COM with kvno 2, encryption type des3-cbc-sha1 added to keytab WRFILE:/var/krb5kdc/test.keytab.
```
 Here, we created a user `test/host@EXAMPLE.COM` and put the key of this user into the file `/var/krb5kdc/test.keytab`.

## Starting KDC
```
 service krb5-kdc start
 * Starting Kerberos KDC krb5kdc       
```

## Performing kinit Authentication
```
kinit -k -t /etc/krb5.keytab test-client/host@EXAMPLE.COM
```
kinit is used to obtain a TGT from KDC. It sends a request to the KDC server specified in `/etc/krb5.conf`. If the TGT is successfully obtained, you can see it by using klist.
```
klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: test-client/host@EXAMPLE.COM

Valid starting       Expires              Service principal
2019-01-15T17:50:25  2019-01-16T17:50:25  krbtgt/EXAMPLE.COM@EXAMPLE.COM
renew until 2019-01-16T00:00:25
```

## Using in a Project
After the kinit authentication succeeds, you can copy the keytab file to the server and client you need to use and configure the corresponding principals to use them.

