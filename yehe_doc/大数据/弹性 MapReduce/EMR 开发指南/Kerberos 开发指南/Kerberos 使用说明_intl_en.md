This document uses MIT's Kerberos as the KDC service and assumes that KDC has been properly installed and started. To use Kerberos, create a realm, add the principals of the relevant roles (including server and client), and generate a keytab file.

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
Add a principal by using kadmin.local.
```
kadmin.local
kadmin.local:  ktadd -k /etc/krb5.keytab test-server/host@EXAMPLE.COM
Entry for principal test-server/host@EXAMPLE.COM with kvno 2, encryption type aes256-cts-hmac-sha1-96 added to keytab WRFILE:/etc/krb5.keytab.
Entry for principal test-server/host@EXAMPLE.COM with kvno 2, encryption type arcfour-hmac added to keytab WRFILE:/etc/krb5.keytab.
Entry for principal test-server/host@EXAMPLE.COM with kvno 2, encryption type des3-cbc-sha1 added to keytab WRFILE:/etc/krb5.keytab.
Entry for principal test-server/host@EXAMPLE.COM with kvno 2, encryption type des-cbc-crc added to keytab WRFILE:/etc/krb5.keytab.
```

## Creating a keytab File
```
kadmin.local
kadmin.local:  ktadd -k /etc/krb5.keytab test-client/host@EXAMPLE.COM
Entry for principal test-client/host@EXAMPLE.COM with kvno 2, encryption type aes256-cts-hmac-sha1-96 added to keytab WRFILE:/etc/krb5.keytab.
Entry for principal test-client/host@EXAMPLE.COM with kvno 2, encryption type arcfour-hmac added to keytab WRFILE:/etc/krb5.keytab.
Entry for principal test-client/host@EXAMPLE.COM with kvno 2, encryption type des3-cbc-sha1 added to keytab WRFILE:/etc/krb5.keytab.
Entry for principal test-client/host@EXAMPLE.COM with kvno 2, encryption type des-cbc-crc added to keytab WRFILE:/etc/krb5.keytab.
kadmin.local:  q
```

Here, we created two users: `test-server/host@EXAMPLE.COM` and `test-client/host@EXAMPLE.COM`. Put their keys into the `/etc/krb5.keytab` file.

## Starting KDC
```
 service krb5-kdc start
 * Starting Kerberos KDC krb5kdc       
```

## Verifying kinit
```
kinit -k -t /etc/krb5.keytab test-client/host@EXAMPLE.COM
```
kinit corresponds to the step of obtaining a TGT from KDC. It sends a request to the KDC server specified in `/etc/krb5.conf`. If the TGT is successfully granted, you can see it by using klist.
```
klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: test-client/host@EXAMPLE.COM

Valid starting       Expires              Service principal
2019-01-15T17:50:25  2019-01-16T17:50:25  krbtgt/EXAMPLE.COM@EXAMPLE.COM
renew until 2019-01-16T00:00:25
```

## Using in a Project
After using kinit to verify the success, you can copy the keytab file to the server and client you need to use and configure the corresponding principals to use them.

