## Overview
When adding nodes to a TKE cluster, you can perform batch operations, such as modification of kernel parameters, by entering a script in **Custom Data**. However, if you need to perform batch operations on existing nodes, you can use the Ansible open-source tool described in this document.


## How It Works
Ansible is a popular open-source OPS tool that can be used to directly perform batch operations on devices over SSH protocol, without the need to manually preinstall dependencies. The following figure shows how it works:
<img style="width:70%" src="https://main.qcloudimg.com/raw/90d1658ff2105497d2ea3a5b54c92bda.png" data-nonescope="true">

## Directions
### Preparing the Ansible control node
1. Select an instance as the Ansible control node, through which batch operations on existing TKE nodes can be initiated. You can select any instance in the VPC where the cluster is located as the control node (including any TKE node).
2. After selecting the control node, select the installation method:
 - For Ubuntu:
``` bash
sudo apt update && sudo apt install software-properties-common -y && sudo apt-add-repository --yes --update ppa:ansible/ansible && sudo apt install ansible -y
```
 - For CentOS:
``` bash
sudo yum install ansible -y
```


### Preparing the configuration file
Add private IPs of all target nodes to the `host.ini` file, with one IP address per line, as shown in the example below:
```
10.0.3.33
10.0.2.4
```
To operate on all nodes, you can run the following commands to generate the `host.ini` file:
``` bash
kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="InternalIP")].address}' | tr ' ' '\n' > hosts.ini
```

### Preparing the batch execution script
Define the batch operations that you want to perform in a script and save it as a script file, as shown in the following example:
A self-built image repository is created, and no certificate has been issued by an authority. It uses the certificate issued by HTTP or HTTPS. By default, an error occurs when dockerd pulls images from this repository. You can perform batch modification of the dockerd configuration on nodes to add the address of the self-built repository to `insecure-registries` in the dockerd configuration. This allows dockerd to ignore the certificate check. The content of the `modify-dockerd.sh` script file is as follows:
```
# yum install -y jq # centos
apt install -y jq # ubuntu
cat /etc/docker/daemon.json | jq '."insecure-registries" += ["myharbor.com"]' > /tmp/daemon.json
cp /tmp/daemon.json /etc/docker/daemon.json
systemctl restart dockerd
```

### Using Ansible to perform batch script execution
Usually, when TKE nodes are added, they all point to the same SSH login key or password. Perform the following operations based on your actual situation:


#### Using a key
1. Prepare a key file, for example, `tke.key`.
2. Run the following command to authorize the key file.
```
chmod 0600 tke.key
```
3. Perform batch script execution.
 - Sample for Ubuntu nodes:
```
ansible all -i hosts.ini --ssh-common-args="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null" --user ubuntu --become --become-user=root --private-key=tke.key -m script -a "modify-dockerd.sh"
```
 - Sample for other operating systems:
```
ansible all -i hosts.ini --ssh-common-args="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null" --user root -m script -a "modify-dockerd.sh"
```


#### Using a password
1. Run the following command to pass a password into a PASS variable.
```
read -s PASS
```
2. Perform batch script execution.
 - For nodes on Ubuntu, the default SSH username is `ubuntu`. See the sample below:
```
ansible all -i hosts.ini --ssh-common-args="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null" --user ubuntu --become --become-user=root -e "ansible_password=$PASS" -m script -a "modify-dockerd.sh"
```
 - For nodes on other operating systems, the default SSH username is `root`. See the sample below:
```
ansible all -i hosts.ini --ssh-common-args="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null" --user root -e "ansible_password=$PASS" -m script -a "modify-dockerd.sh"
```
