# NIS_and_NFS - Client_Configuration

In "sales.inova.pt" and "marketing.inova.pt" after having made NIS and NFS

# **In Termius**

## **NFS**

◻️ Go to super user `sudo su -`;

◻️ `nano /etc/hosts` Inside that text document you will insert the following code (code that will associate the IP to the respective names) `192.168.2.150 central.inova.pt central inova.pt` ;

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

◻️ Update and upgrade your client `apt update -y && apt upgrade -y` ❓ In case of doubt, the "&&" serves as an "and", as an example the previous code is to update "and" upgrade;

◻️ After doing the update and upgrade, NFS will be installed `apt install nfs-common -y`;

◻️ After the installation you will create a folder with the same name that was created on the server `mkdir /mnt/user`;

◻️ `mount -t nfs 192.168.2.150:/mnt/user /mnt/user/` ;

◻️ `cat /etc/mtab` (copy last line to `/etc/fstab` and add ,nofail)

## **NIS**

◻️ `apt -y install nis` ;

NIS domain
```
inova.pt
```
◻️ `nano /etc/yp.conf` add at the end `domain inova.pt server central.inova.pt` ;

◻️ `nano /etc/nsswitch.conf` ⤵️

![nis8](https://user-images.githubusercontent.com/48421530/153508426-e05b40aa-f40f-4c77-91a9-dd921660d26c.png)

◻️ `nano /etc/pam.d/common-session`  add to the end: set follows if needed (create home directory automatically if none) session optional
`session optional        pam_mkhomedir.so skel=/etc/skel umask=077`;

◻️ `systemctl restart nis` log in to see if it's working.
