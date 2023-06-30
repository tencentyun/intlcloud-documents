## Introduction
Advanced Package Tool (APT) is a free software user interface that works with core libraries to handle the installation and removal of software on various Linux distributions. APT offers a centralized interface for software management and a better experience than having to download and install software one by one. Tencent Cloud hosts APT sources so you can install software without adding sources.

## Prerequisites
Log in to a Linux CVM instance that runs Ubuntu.

## Directions
> In the following, Nginx is used as an example.
>

### Listing available software
Run the following command to list available software:
```
sudo apt-cache search all
```

### Installing software
Run the following command to install Nginx: 
```
sudo apt-get install nginx
```
Make sure this is the software you want to install and enter `Y` to approve the installation. Wait until the software installation is complete, as shown in the figure below:
![](https://mc.qcloudimg.com/static/img/d03f55bba1690ff30532b73148ccc1e9/45.png)

### Querying installed software
You can run different commands to query installed software.
- Run the following command to query the directory of the software package and all the files in the software package.
``` 
sudo dpkg -L software_name 
```
- Run the following command to query the version information of the software package.
``` 
sudo dpkg -l software_name 
```

View information on the installed Nginx, as shown in the figure below:
![](https://mc.qcloudimg.com/static/img/8bbc99d7a31e8463da36f3dc2221c028/46.png)
