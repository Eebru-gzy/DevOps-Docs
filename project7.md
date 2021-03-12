# **Introduction**
* This task introduces an architecture that requires the use of different servers to archive different purposes:

  * NFS Server: 1 quantity. The server that hosts the web applications files as well as web logs.
  * Database Server: 1 quantity. The server that the database would be on.
  * Web Server: 3 quantity. The servers that host the   web application.

## **Initializing the NFS Server**
* This server serves as the ‘single point of truth’ for the application, all the files and directories that the web-servers would need would be domiciled here.
* I spun up the EC2 instance from AWS and I added 3 block storage volumes of 1GB each to the server.
* I ssh into it.

## **Making Logical Volumes from the Block Storages**
* Using the `MBR's fdisk utility` I created a partition of type LVM (8e) on all the block volumes.
* I made physical volumes of for web apps at `/mnt/apps`, web logs at `/mnt/logs` and opt at `/mnt/opt`
![logical volume](./p7/making-lv.png)
* I also made sure these mount points are always mounting when the system boots by add entry to the `/etc/fstab` file.
* Below is the output of the `mount` command.
![mount points](./p7/lv-mounts.png)


## **Installing NFS Server, and configure to start on system boot**
* `sudo yum update` to update the system depenedencies.
* `sudo yum install nfs-utils -y` to install nfs and its dependencies
![nfs install](./p7/nfs-install.png)
* `sudo systemctl start nfs-server` to start the nfs service
* `sudo systemctl enable nfs-server` to make sure the nfs service starts on boot up
* `sudo systemctl status nfs-server` shows the status of the nfs service running.
![nfs install](./p7/started-enabled-NFS.png)

## **Setting permission on the mount points for web servers accessibility**