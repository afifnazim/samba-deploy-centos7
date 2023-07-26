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
mkdir /share-directory
chmod -R 777 /share-directory
```

### Configuring share
The main configure file is located under /etc/samba. We can open the file using <b><i>vim</i></b> editor and append the following to this file <b><i>/etc/samba/smb.conf</i></b>
```
vim /etc/samba/smb.conf

[myshare]
        comment = Samba Share Directory
        path = /share-directory
        read only = No
```

### Create Samba User
Then we will create samba user 
```
smbpasswd -a user

New SMB password:
Retype new SMB password:
```

### Configure SELinux
We will need to configure SELinux on the samba shared directory
```
semanage fcontext -a -t samba_share_t "/share(/.*)?"
restorecon -R -v /share
```

### Start smb services
We will start and enable smb and nmb services in the server side 
```
systemctl enable smb
systemctl start smb
systemctl enable nmb
systemctl start nmb
```
### Add rule in firewalld 
If we are using firewalld in the server then we need to add rule to allow samba ports 
```
smbclient -U <samba username we created above> -L <ip address of server>
```

### Test 
We can test by adding the shared directory in any of the windows system by using username and password. 
