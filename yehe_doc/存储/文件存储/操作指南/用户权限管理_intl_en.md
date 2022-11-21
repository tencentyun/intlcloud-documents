This document describes how to set the access permissions of users and user groups based on the POSIX syntax in a file system, which can be Standard (NFS), High-Performance (NFS), Standard Turbo, or High-Performance Turbo. 

## Prerequisites

You have mounted the file system over the Turbo or NFSv3 protocol as instructed in [Using CFS Turbo on Linux Clients](https://www.tencentcloud.com/document/product/582/40298) or [Using CFS File Systems on Linux Clients](https://www.tencentcloud.com/document/product/582/11523).

## Command description

| Command | Description |
|---------|---------|
| getfacl &lt;filename> | View the current ACL of the file. |
| setfacl -m g:cfsgroup:w &lt;filename> | Set the write permission for the `cfsgroup` user group. |
| setfacl -m u:cfsuser:w &lt;filename> | Set the write permission for the `cfsuser` user. |
| setfacl -x g:cfsgroup &lt;filename> | Delete the permission of the `players` user group. |
| getfacl file1 \| setfacl --set-file=- file2 | Copy the ACL of the `file1` file to the `file2` file.  |
| setfacl -b file1 | Delete all extended ACL rules and retain basic ACL rules (owner, group, and others).  |
| setfacl -k file1 | Delete all default rules from the `file1` file.  |
| setfacl -R -m g:cfsgroup:rw dir | Add the read/write permission of the `cfsgroup` user group to the files and directories in the `dir` directory tree. |
| setfacl -d -m g:cfsgroup:rw dir | Set the read/write permission of the `cfsgroup` user group for the newly created files and directories in the `dir` directory tree.  |


## Examples

```
sudo useradd cfsuser  # Create the `cfsuser` user
sudo useradd otheruser  # Create the `otheruser` user
sudo groupadd cfsgroup  # Create the `cfsgroup` user group
sudo usermod -g cfsgroup cfsuser  # Allocate `cfsuser` to `cfsgroup`
sudo touch file1 # Create a file named `file1`
sudo setfacl -m g:cfsgroup:r-x file1 # Grant the `cfsgroup` user group the permission to read and execute `file1`
sudo setfacl -m u:otheruser:rwx dir0 # Grant the `otheruser` user the permission to read/write and execute `file1`
```

