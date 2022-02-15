# NIS_and_NFS - Server_Configuration

### In "central.inova.pt" after having made RAID-5

# In Termius

## NFS

◻️ Go to super user `sudo su -`;

◻️ `nano /etc/hosts` Inside that folder you will insert the following code (code that will associate the IP to the respective names) `192.168.2.150 central.inova.pt central inova.pt` ;

```
127.0.0.1 localhost
192.168.2.150 central.inova.pt central inova.pt
# The following lines are desirable for IPv6 capable hosts
::1 ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
```

◻️ Update and upgrade your server `apt update -y && apt upgrade -y` ❓ In case of doubt, the "&&" serves as an "and", as an example the previous code is to update "and" upgrade;

◻️ After doing the update and upgrade, NFS will be installed `apt install nfs-kernel-server`;

◻️ After the installation you will create a folder where you will contain your users, for example: `mkdir /mnt/user`;

◻️ `nano /etc/exports` Add the following line at the end of the document `/mnt/user *(rw,sync,no_subtree_check,no_root_squash)`

```
# /etc/exports: the access control list for filesystems which may be exported
#               to NFS clients.  See exports(5).
#
# Example for NFSv2 and NFSv3:
# /srv/homes       hostname1(rw,sync,no_subtree_check) hostname2(ro,sync,no_subtree_che>
#
# Example for NFSv4:
# /srv/nfs4        gss/krb5i(rw,sync,fsid=0,crossmnt,no_subtree_check)
# /srv/nfs4/homes  gss/krb5i(rw,sync,no_subtree_check)
#
/mnt/user *(rw,sync,no_subtree_check,no_root_squash)
```

and pay attention, if you have changed the name of the folder and the site, change the `/mnt/user ...` for the correct alternaive;

◻️ `exportfs -a` serves to implement the line that was placed in the `nano /etc/export`;

◻️ After all that, enable NFS service `systemctl enable --now nfs-kernel-server`.

### Add users to folder `/mnt/user`.

◻️ `adduser sales --home /mnt/user/sales` ;

◻️ `adduser marketing --home /mnt/user/marketing` ;

◻️ `echo xfce4-session > /mnt/user/marketing/.xsession` ;

◻️ `echo xfce4-session > /mnt/user/sales/.xsession` ;

◻️ `chown sales:sales /mnt/user/sales/.xsession` ;

◻️ `chown marketing:marketing /mnt/user/marketing/.xsession` ;

> You can add more users, just change the `sales` or `marketing` to any other name of your choice.

## **NIS**

◻️ `apt -y install nis`

NIS domain
```
inova.pt
```
◻️ `nano /etc/default/nis` change from false to master, as it can be seen on the following image ⤵️

![nis2](https://user-images.githubusercontent.com/48421530/153502445-ea878e6b-b3f6-460a-9032-57308b469b5a.png)

◻️ `nano /etc/yp.conf` add at the end `domain inova.pt server central.inova.pt` ;

◻️ `nano /etc/ypserv.securenets` 

Comment:
```
0.0.0.0      0.0.0.0
``` 
And change to:
```
255.255.0.0      192.168.0.0
```

◻️ `nano /var/yp/Makefile` change from false to true the lines 52 and 56 ⤵️

![nis4](https://user-images.githubusercontent.com/48421530/153503160-14597768-bb4a-464c-acad-c4e8518e333c.png)

◻️ `/usr/lib/yp/ypinit -m`

![nis 5](https://user-images.githubusercontent.com/48421530/153504412-bda4b4b1-cbd6-4947-b944-3568a2bf0ba9.png)

◻️ `systemctl restart nis` and `systemctl status nis` to see if the nis is working

◻️ `cd /var/yp` and `make`
