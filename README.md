# umbrel.memories
 Logs and problems I encountered Including solving various problems. in use umbrel lightning node.
 
After I've been using umbrel for a while. For 1 year I have been using it, I have never turned it off. and it's never been a problem. until one day I have moved the location of the node run. Then it started having access issues. I think I should save it. so that in the future I may have to use it again. And this may help you get through the chaos that may happen to you.

## login problem

If you are having trouble logging in. For me, I use A2F for security. But now I can't access it, although my A2F code is absolutely correct. Including time update with Google. So, How do we solve it?

If unable to login from the web page. But, You can also access the umbrel via the command line, And you can access your node via SSH. Let you do the following.

1. Open your terminal, then enter the following commands : `ssh umbrel@umbrel.local` or `ssh umbrel@(ip address of umbrel node)`
2. Answer "yes" to confirm.
3. Enter your umbrel node password.
4. Edit `dhcpcd.conf` by the command `sudo nano /etc/dhcpcd.conf`
6. Add these notes to the bottom of the file.

~~~
#Configuration static IP address (CHANGE THE VALUES TO FIT FOR YOUR NETWORK)
interface eth0
static ip_address=192.168.1.xxx/24
static routers=192.168.1.1
static domain_name_servers=8.8.8.8, 8.8.4.4
~~~

7. Restart networking system by the command `sudo /etc/init.d/networking restart`
8. Log in via the web page again. hope to succeed

**NOTE** : Disconnecting the power supply is incorrect and should not be done. sudden disconnection of power supply This directly destroys your SSD. and you should avoid

## Raspberry Pi Task Manager

You can view the processes running in the background using the command `htop`

![pic1](/src/Screenshot%20from%202022-11-25%2013-01-58.png)

## Uninstall umbrel from ubuntu

I've tested installing umbrel on ubuntu 22.04. But I'm facing insufficient space to store all blocks. and I tried to uninstall it. in umbrel.comunication There is little information for me to delete the /home/umbrel directory. It can't be easily done, I deleted it with Shift+Del and after a while the directory was back in place.

Finally I discovered that Docker is still running so that when deleting the directory it can always be recreated like salamander. So I had to stop Docker first with the command `sudo systemctl stop docker` Then the `/home/umbrel` directory can be removed.

~~~
sudo rm -rf umbrel
~~~

## Raspberry Pi Basic Command

- Update Raspberry OS (Don't use it with your umbrel)
~~~
sudo apt-get update 
sudo apt-get upgrade
~~~
- Access Raspberry Pi Configuration (Don't use it with your umbrel)
~~~
sudo raspi-config
~~~
- Network Configuration Details
~~~
ifconfig
~~~
- Restart Your Raspberry Pi
~~~
sudo reboot
~~~
- Power Off Raspberry Pi
~~~
sudo shutdown -h now
~~~
- List Files and Directories
~~~
ls
~~~
- Find a File
~~~
find / -name filename
~~~
- Check Current Directory
~~~
pwd
~~~
- Download a File
~~~
wget URL
~~~
- Install a Program
~~~
sudo apt-get install programname
~~~
- Run a Script
~~~
chmod a+x filename.sh
./filename.sh
~~~
- Elevated Permission
~~~
sudo su
~~~
- Change File Ownership
~~~
sudo chown pi:root filename
~~~
- Extract Files
~~~
unzip filename
~~~
- Extract TAR Files
~~~
tar -cvzf filename.tar.gz
~~~
Remove a Package
~~~
sudo apt-get remove packagename
~~~
- Scan the Local Network
~~~
sudo apt-get install nmap
nmap -sn 192.168.1.0/24
~~~
- Find the IP Address of Raspberry Pi
~~~
hostname -I
~~~
- View Background Tasks
~~~
htop
~~~
- Check Raspberry OS Version
~~~
cat /proc/version
~~~
- Check Hardware Information
~~~
lscpu
cat /proc/meminfo
cat /proc/partitions
~~~

## 
