# Boot from grub command line

Sometimes it could happen you have some troubles during the boot of your Linux OS. In order to avoid the problem a procedure for booting the system from the GRUB console is following:

first of all set the pager

```bash
grub> set pager=1

```

after that, you have to check for the partition in which you have installed the Linux OS. Starting with the `ls` command try to find the OS partition. You should obtain a list like `(hd0, 1) (hd0, gptX)`. Explore the contents until you find something like this:

```bash
grub> ls (hd0,1)/

```
output:
```
lost+found/ bin/ boot/ cdrom/ dev/ etc/ home/  lib/
lib64/ media/ mnt/ opt/ proc/ root/ run/ sbin/ 
srv/ sys/ tmp/ usr/ var/ vmlinuz vmlinuz.old 
initrd.img initrd.img.old

```

Now check the correctness:

```bash
grub> cat (hd0,1)/etc/issue
```
output:

Ubuntu 14.04 LTS \n \l

```

Once you have discovered the right partition and the right OS, you will follow these procedure in order to boot the system:

```bash
grub> set root=(hd0,1)
grub> linux /boot/vmlinuz-3.13.0-29-generic root=/dev/sda1
grub> initrd /boot/initrd.img-3.13.0-29-generic
grub> boot

```

N.B. If you want to be sure of the root for the linux kernel, check the fstab file:

```bash
grub> set root=(hd0,1)
grub> cat /etc/fstab

```
