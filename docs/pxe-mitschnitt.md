b## 2022-03-08, lp5jvogel
## Slitaz per PXE / Debian 11
## DHCP SERVER in Betrieb nehmen
apt update
apt install isc-dhcp-server
vi /etc/dhcp/dhcpd.conf
# ACHTUNG: Mac-Adresse anpassen!
----8<-------8<----- /etc/dhcp/dhcpd.conf
authoritative;
subnet 192.168.0.0 netmask 255.255.255.0  {
}

host client {
   fixed-address 192.168.0.10;
   hardware ethernet 08:00:27:e8:30:46;
   option routers 192.168.0.1;
   option host-name "client";
   next-server 192.168.0.1;
   filename "gpxelinux.0";
}
---->8------->8----- /etc/dhcp/dhcpd.conf
ip a add 192.168.0.10/24 up dev enp0s3
service isc-dhcp-server restart


## TFTP SERVER in Betrieb nehmen
apt install tftpd
mkdir /srv/tftp

## PXELinux in Betrieb nehmen
apt install pxelinux syslinux-common
cp /usr/lib/PXELINUX/gpxelinux.0 /srv/tftp/.
cp /usr/lib/syslinux/modules/bios/ldlinux.c32 /srv/tftp/.
mkdir /srv/tftp/pxelinux.cfg
vi /srv/tftp/pxelinux.cfg/default
----8<----8<-- /srv/tftp/pxelinux.cfg/default
default slitaz
prompt 0
label slitaz
    menu label Slitaz
    kernel slitaz/bzImage
    append initrd=slitaz/rootfs4.gz,slitaz/rootfs3.gz,slitaz/rootfs2.gz,slitaz/rootfs1.gz rw root=/dev/null vga=normal autologin
---->8---->8-- /srv/tftp/pxelinux.cfg/default

## Slitaz an den richtigen Ort kopieren
cd ~
wget http://mirror.slitaz.org/iso/4.0/slitaz-4.0.iso
mount -o loop slitaz-4.0.iso /mnt
mkdir /srv/tftp/slitaz
cp /mnt/boot/bzImage /mnt/boot/rootfs* /srv/tftp/slitaz/.
umount /mnt

## alles eingerichtet, jetzt Client booten