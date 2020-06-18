For a formal production system with Kerberos enabled, you should also consider the high availability (HA) of KDC. The Kerberos service can be configured as master/slave mode where data is synced from the master node to the slave node through the kprop service. After an EMR HA cluster is purchased, Kerberos is highly available by default with no additional configuration required.

This document describes how to configure and use HA for the Kerberos service.

## Prerequisites
- You have purchased an EMR HA cluster.
- You enabled Kerberos authentication when purchasing the cluster.

## KDC HA Configuration Overview

Configure the `/etc/krb5.conf` file as follows:
>Two KDC addresses are configured in the example: `active kdc` and `backup kdc`, so as to ensure that when either KDC service is exceptional, normal KDC service can still be provided for the cluster.
>
```
[libdefaults]
dns_lookup_realm = false
ticket_lifetime = 24h
renew_lifetime = 7d
forwardable = true
rdns = false
default_realm = REALM
default_tgs_enctypes = des3-cbc-sha1
default_tkt_enctypes = des3-cbc-sha1
permitted_enctypes = des3-cbc-sha1

[realms]
REALM = {
kdc = active_kdc:88
admin_server = active_kdc
kdc = backup_kdc:88
admin_server = backup_kdc 
}

[domain_realm]
# .example.com = EXAMPLE.COM
```

## KDC Data Sync
-  kprop configuration
There is a `/var/kerberos/krb5kdc/kpropd.acl` configuration file on both the KDC servers by default.
```
host/active_kdc@REALM
host/backup_kdc@REALM
```
2. Execute the `/var/kerberos/krb5kdc/kpropd.acl` file.
After executing the default configuration file `/var/kerberos/krb5kdc/kpropd.acl`, a `/etc/krb5.keyta` file will be generated on both the KDC servers. At the same time, the two KDC servers will also start the kprop service.
```
[root@10 krb5kdc]# service kprop status 
Redirecting to /bin/systemctl status kprop.service
kprop.service - Kerberos 5 Propagation
Loaded: loaded (/usr/lib/systemd/system/kprop.service; disabled; vendor preset: disabled)
Active: active (running) since Thu 2020-05-07 15:33:35 CST; 1h 9min ago
Process: 3752 ExecStart=/usr/sbin/_kpropd $KPROPD_ARGS (code=exited, status=0/SUCCESS)
Main PID: 3753 (kpropd)
CGroup: /system.slice/kprop.service
└─3753 /usr/sbin/kpropd
```
4. Run the regular KDC data sync command
The EMR agent will regularly (once every five minutes by default) sync the `principals` of `active kdc` to `backup kdc` to ensure that the data on the two KDC servers are in sync. The following sync command will be executed regularly on `active kdc`:
```
kdb5_util dump /var/kerberos/krb5kdc/master.dump & kprop -f /var/kerberos/krb5kdc/master.dump -d -P 754 backup_kdc
```

## Result Verification

1. Run the following command on `active kdc`.
```
kadmin.local "-q addprinc -randkey test"
```
2. You can see the newly added `principal` on `backup kdc`, indicating that the data sync between the two KDC servers has been completed. This operation takes a while (five minutes by default).
```
kadmin.local "-q listprincs"|grep test
```

 
