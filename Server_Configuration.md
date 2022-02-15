# NIS_and_NFS - Server_Configuration

# In AWS

🔴 1 Instance (Server);

🔴 1 Elastic IP (for instance).

# In Termius

## NFS

◻️ First define the server name, for example: `sudo hostnamectl set-hostname example.example.com`;

◻️ Go to super user `sudo su -`;

◻️ `nano /etc/hosts` Inside that folder you will insert the following code (code that will associate the IP to the respective names) `x.x.x.x example.example.com example example.com` (“x.x.x.x” is Private IP Server);

```
127.0.0.1 localhost
x.x.x.x example.example.com example example.com
# The following lines are desirable for IPv6 capable hosts
::1 ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
```

◻️ Update and upgrade your server `apt update && apt upgrade` ❓ In case of doubt, the "&&" serves as an "and", as an example the previous code is to update "and" upgrade;

◻️ After doing the update and upgrade, NFS will be installed `apt install nfs-kernel-server`;

◻️ After the installation you will create a folder where you will contain your users, for example: `mkdir /var/homes`;

◻️ `nano /etc/exports` Add the following line at the end of the document `/var/homes *(rw,sync,no_subtree_check,no_root_squash)`

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
/var/homes *(rw,sync,no_subtree_check,no_root_squash)
```

and pay attention, if you have changed the name of the folder and the site, change the `/var/homes ...` for the correct alternaive;

◻️ `exportfs -a` serves to implement the line that was placed in the `nano /etc/export`;

◻️ After all that, enable NFS service `systemctl enable --now nfs-kernel-server`.

### Add users to folder `/etc/hosts`.

◻️ `adduser user --home /var/homes/user`;

◻️ `echo xfce4-session > /var/homes/user/.xsession`;

◻️ `chown user:user /var/homes/user/.xsession`;

> You can add more users, just change the `user` to any other name of your choice.

## **NIS**

◻️ `apt -y install nis`

![NIS](https://user-images.githubusercontent.com/48421530/153502048-ea7272a1-3665-4289-8c7f-a6b7790b9f09.png)

◻️ `nano /etc/default/nis` change from false to master, as it can be seen on the following image ⤵️

![nis2](https://user-images.githubusercontent.com/48421530/153502445-ea878e6b-b3f6-460a-9032-57308b469b5a.png)

◻️ `nano /etc/yp.conf` ⤵️

![nis 6](https://user-images.githubusercontent.com/48421530/153504762-3f2614c4-c447-4cef-b5b8-5bed63f069e6.png)

◻️ `nano /etc/ypserv.securenets` ⤵️

![nis3](https://user-images.githubusercontent.com/48421530/153503129-5cfe6ba2-227f-4bfe-9dca-0695ba854a10.png)

◻️ `nano /var/yp/Makefile` change from false to true the lines 52 and 56 ⤵️

![nis4](https://user-images.githubusercontent.com/48421530/153503160-14597768-bb4a-464c-acad-c4e8518e333c.png)

◻️ `/usr/lib/yp/ypinit -m`

![nis 5](https://user-images.githubusercontent.com/48421530/153504412-bda4b4b1-cbd6-4947-b944-3568a2bf0ba9.png)

◻️ `systemctl restart nis` and `systemctl status nis` to see if the nis is working

◻️ `cd /var/yp` and `make`
