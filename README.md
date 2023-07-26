# samba-deploy-centos7
Documenting the process of Samba file sharing system in centOS 7 system

We use samba service to share files between Linux and Windows systems. Samba uses the SMB (Server Message Block) protocol to share files. We will use the CentOS 7 as the SMB server and install the services. 

### Samba Installation 
To install samba packages we can use the below command -
```
yum install samba samba-client samba-common -y
```

### Create Directory to share
We need to create a shared directory and provide required permission to that directory. We will provide read, write and execute permission -
```
mkdir /share
chmod -R 777 /share
```

### Configuring share
The main configure file is located under /etc/samba. We can open the file using <b><i>vim</i></b> editor and append the following to this file <b><i>/etc/samba/smb.conf</i></b>
```
vim /etc/samba/smb.conf

[myshare]
        comment = My share
        path = /share
        read only = No
```
