# NIS_and_NFS - Server_Configuration

# **In AWS**

🔴 1 Instances (Server);

🔴 1 Elastic IPs (for each instance).

# **In Termius**

## **NFS**

◻️ First define the server name, for example: `sudo hostnamectl set-hostname example.example.com`;

◻️ Go to super user `sudo su -`;

◻️ `nano /etc/hosts` Inside that folder you will place the following code (code that will associate the IP to the respective names) `x.x.x.x example.example.com example example.com` (“x.x.x.x” is Private IP Server);

◻️ Update and upgrade your server `apt update && apt upgrade` ❓ In case of doubt, the "&&" serves as an "and", as an example the previous code is to update "and" upgrade;

◻️ After doing update and upgrade, NFS will be installed `apt install nfs-kernel-server`;

◻️ After installation you will create a folder where you will contain your users, for example: `mkdir /var/homes`;

◻️ `nano /etc/export` Add the following line at the end of the document `/var/homes *(rw,sync,no_subtree_check,no_root_squash)` and pay attention, if you have changed the name of the folder and the site, change what says `/var/homes ...` for the respective change;

◻️ `exportfs -a` serve para implementar a linha que foi colocada no `nano /etc/export`;

◻️ After all that, enable NFS service `systemctl enable --now nfs-kernel-server`.

### Add users to folder `/etc/hosts`.

◻️ `adduser user --home /var/homes/user`;

◻️ `echo xfce4-session > /var/homes/user/.xsession`;

◻️ `chown user:user /var/homes/user/.xsession`;

> You can add more users, just change the `user` to any other name of your choice.

## **NIS**

◻️ `apt -y install nis`

◻️ `nano /etc/default/nis`

◻️ `nano /etc/ypserv.securenets`

◻️ `nano /var/yp/Makefile`

◻️ `/usr/lib/yp/ypinit -m`

◻️ `systemctl restart nis` and `systemctl status nis` para visualizar se o nis está a funcionar

◻️ `cd /var/yp` and `make`

◻️

◻️






