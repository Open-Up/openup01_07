# Practical work on file systems

During this practical work, we are going to use filesystems.

## Playing with partitions

As we will not work with local disks (too dangerous), we are going to use a file, wich will be used as disk.

To create the file : 

```
sudo dd if=/dev/zero of=/root/diskimage bs=1M count=256
```

We can now format it with a file system : 

```
sudo mkfs.ext4 /root/diskimage
```

Now we will pretend it is a device, so that is shows up in /dev :

```
sudo losetup /dev/loop9 /root/diskimage
```

Question 1: 

 - mount it in /mnt/loop0.

 - Create a file in it

 - print all the mounted partitions

 - unmount this file system

We now want two partitions. A first one of 64MB will be formatted as FAT. A second one will be formatted as EXT-4 and will have a size of 196 MB.

Question 2:

 - Why would I want to use two partitions like this? Do you have a real world example?

 - Run fdisk on /dev/loop9, and create the given partitions

 - We now need to map in devices the created partitions. To do this :

```
kpartx -v -a /root/diskimage
```

 - Format the given devices.

 - Run fsck on them to correct possible errors

 - Mount them in /mnt/p1 and /mnt/p2

## Playing with swap

 - Add 1GB of swap to the machine. You will do it thanks to a file named /root/swap

## Informations about a device

Give the following informations about /dev/mapper/loop9p2 : 

 - Number of free inodes

 - Number of free blocks

 - Block size

 - Last mount + mounted directory

 - Number of mount

 - UID + magic number for this filesystem

Can you give the same informations for /dev/mapper/loop9p1 ? Why?

## Playing with links

 - Create a file /mnt/p1/d1/f1

 - Create a hard link /mnt/p1/d2/f2 to /mnt/p1/d1/f1 . Read the content of the link.

 - What are the number of inodes of /mnt/p1/d1/f1 and /mnt/p1/d2/f2 ? Why ?

-----------------------

 - Create a soft link /mnt/p1/d2/soft to /mnt/p1/d1/f1 . Read the content of the link.

 - What are the number of inodes of /mnt/p1/d1/f1 and /mnt/p1/d2/soft ? Why ?

-----------------------

 - Can I create a hard link from /mnt/p1/d1/f1 to /mnt/p2/d1/f1 ? Why ?

 - Create a soft link /mnt/p2/d2/soft to /mnt/p1/d1/f1 . Read the content of the link.

 - Remove /mnt/p1/d1/f1. Are the links still here ? Can you read there content ? Why ?

## Clean up

 - unmount all the directories in /mnt 

 - Delete the files /root/diskimage and /root/swap
