# NIS_and_NFS - Client_Configuration

# **In AWS**

🔴 1 Instance (Client);

🔴 1 Elastic IP (for each instance).

# **In Termius**

## **NFS**

◻️ First define the server name, for example: `sudo hostnamectl set-hostname client.example.com`;

◻️ Go to super user `sudo su -`;

◻️ `nano /etc/hosts` Inside that folder you will place the following code (code that will associate the IP to the respective names) `x.x.x.x example.example.com example example.com` (“x.x.x.x” is Private IP Server);

![nis7](https://user-images.githubusercontent.com/48421530/153506257-deca5eb7-28f4-4671-9359-0a4d65f885d7.png)

◻️ Update and upgrade your client `apt update && apt upgrade` ❓ In case of doubt, the "&&" serves as an "and", as an example the previous code is to update "and" upgrade;

◻️ After doing update and upgrade, NFS will be installed `apt install nfs-common`;

◻️ After installation you will create a folder with the same name that was created on the server `mkdir /var/homes`;

◻️ `mount -t nfs x.x.x.x:/var/homes /var/homes/` (“x.x.x.x” is Private IP SRV);

◻️ `cat /etc/mtab` (copy last line to `/etc/fstab` and add ,nofail)

## **NIS**

◻️ `apt -y install nis` ⤵️

![NIS](https://user-images.githubusercontent.com/48421530/153502048-ea7272a1-3665-4289-8c7f-a6b7790b9f09.png)

◻️ `nano /etc/yp.conf` ⤵️

![nis 6](https://user-images.githubusercontent.com/48421530/153504762-3f2614c4-c447-4cef-b5b8-5bed63f069e6.png)

◻️ `nano /etc/nsswitch.conf` ⤵️

![nis8](https://user-images.githubusercontent.com/48421530/153508426-e05b40aa-f40f-4c77-91a9-dd921660d26c.png)

◻️ `nano /etc/pam.d/common-session`  add to the end: set follows if needed (create home directory automatically if none) session optional
`session optional        pam_mkhomedir.so skel=/etc/skel umask=077`;

◻️ `systemctl restart nis` log in to see if it's working.
