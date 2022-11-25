# vsftpd


## Prerequisites

Access to a user account with sudo privileges
Access to a terminal window/command line (Ctrl-Alt-T)
The apt package manager, included by default


## Step 1: Update System Packages
Start by updating your repositories – enter the following in a terminal window:

```
sudo apt update
```

## Step 2: Install vsftpd Server on Ubuntu
A common open-source FTP utility used in Ubuntu is vsftpd. It is recommended for its ease of use.

1. To install vsftpd, enter the command:

```
sudo apt install vsftpd
```

2. To launch the service and enable it at startup, run the commands:

```
sudo systemctl start vsftpd

sudo systemctl enable vsftpd
```

## Step 3: Backup Configuration Files
Before making any changes, make sure to back up your configuration files.

1. Create a backup copy of the default configuration file by entering the following:

```
sudo cp /etc/vsftpd.conf  /etc/vsftpd.conf_default
```

## Step 4: Create FTP User

Create a new FTP user with the following commands:

```
sudo useradd -m testuser

sudo passwd testuser
```

## Step 6: Connect to Ubuntu FTP Server
Connect to the FTP server with the following command:
```
sudo ftp ubuntu-ftp
```
Replace ubuntu-ftp with the name of your system (taken from the command line).

Log in using the testuser account and password you just set. You should now be successfully logged in to your FTP server.



## Configuring and Securing Ubuntu vsftpd Server

Change Default Directory
By default, the FTP server uses the /srv/ftp directory as the default directory. You can change this by creating a new directory and changing the FTP user home directory.

To change the FTP home directory, enter the following:

```
sudo mkdir /srv/ftp/new_location

sudo usermod -d /srv/ftp/new_location ftp
```

Restart the vsftpd service to apply the changes:

```
sudo systemctl restart vsftpd.service
```
Now, you can put any files you want to share via FTP into the /srv/ftp folder (if you left it as the default), or the /srv/ftp/new_location/ directory (if you changed it).



## Authenticate FTP Users
If you want to let authenticated users upload files, edit the vsftpd.conf file by entering the following:

```
sudo nano /etc/vsftpd.conf
```

Find the entry labeled write_enable=NO, and change the value to “YES.”


Save the file, exit, then restart the FTP service with the following:

```
sudo systemctl restart vsftpd.service
```


## Securing FTP
Numerous exploits take advantage of unsecured FTP servers. In response, there are several configuration options in vsftpd.conf that can help secure your FTP server.

Limit User Access
One method is to limit users to their home directory. Open vsftpd.conf in an editor and uncomment the following command:

```
chroot_local_user=YES
```

