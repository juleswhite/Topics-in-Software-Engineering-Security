
Useful changes to the Vagrantfile

Change these in Vagrantfile:

\# Add a known address that we can get into the VM from
config.vm.network "private_network", ip: "192.168.2.2"
\# Automatically deploy everything from ./deploy to /homne/vagrant/deploy on the guest
config.vm.provision "file", source: "./deploy", destination: "/home/vagrant/deploy"

Reload the changes:
vagrant reload --provision

Starting Vagrant
vagrant up

SSHing into Vagrant

vagrant ssh
SSH
Connect to remote machines
In this case, connecting to local VM

Host Configuration
Anything prefixed with "#" is a comment

Find and install packages
Apache

apt-cache search apache
#or
apt-cache search apache | grep apache

sudo apt-get install apache2


List installed packages
apt list --installed

List files installed by package
dpkg -L apache2

Users

Current user
whoami

Execute a command as super user
sudo <cmd>

Execute a command as if you are another user (www-data)
sudo -u www-data find /var/ -type f -executable

List all users
awk -F: '{ print $1}' /etc/passwd

List logged in users
w
w vagrant
who 
users

See the last time someone logged in
last
lastlog

Add user
useradd -m -d /home/bob bob

Set their password
passwd bob

Add bob to the sudo group
usermod -a -G sudo bob

Switch to another user
su bob

Add detailed auditing of users
sudo apt-get install acct

Audit user
sudo lastcomm vagrant

Who was the last person to add a user
sudo lastcomm useradd

Data

Change directory
cd /home/vagrant

Display file contents
cat /home/vagrant/.bash_history

Other ways to see file contents interactively
more /home/vagrant/.bash_history

Follow a file as it changes
tail -f /home/vagrant/.bash_history

Quickly create a file by echoing output into it
echo "echo bob" > ./somefile

Edit a file with vi
Beyond the scope of this tutorial, go see https://www.tutorialspoint.com/unix/unix-vi-editor.htm

To escape vi, you can always type "ESC", then ":q!"
List files and permissions

ls -alt /home/vagrant
Linux file permissions

drwxr-xr-x 4 vagrant vagrant 4096 Jun 20 20:02 .
-rw------- 1 vagrant vagrant   65 Jun 20 20:02 .bash_history
drwx------ 2 vagrant vagrant 4096 Jun 20 20:00 .ssh
drwx------ 2 vagrant vagrant 4096 Jun 20 20:00 .cache
drwxr-xr-x 4 root    root    4096 Jun 20 20:00 ..
-rw-r--r-- 1 vagrant vagrant  220 Apr 11 08:32 .bash_logout
-rw-r--r-- 1 vagrant vagrant 3771 Apr 11 08:32 .bashrc
-rw-r--r-- 1 vagrant vagrant  655 Apr 11 08:32 .profile

[Is Dir?][Is Sym Link?][User Read][User Write][User Exec][Group Read][Group Write][Group Exec][Others Read][Others Write][Others Exec] [Ignore] [Owner] [Group]

Add execute permission to file for current user
chmod +x /home/vagrant/deploy/hello.txt

Remove write and execute permission from file for group
chmod g-xw /home/vagrant/deploy/hello.txt

Remove read,write,execute permission from file for others
chmod o-rxw /home/vagrant/deploy/hello.txt

See what files are owned by user / group
sudo find /var/ -user www-data

See what files someone can write to
find /etc -type f -readable

See what files another user can execute
sudo -u www-data find /var/ -type f -executable

Running Instructions / Processes

List running processes
ps -few

Process ID
User of the process
Group of the user
Permissions of the group

Where did that process come from
sudo ls -l /proc/<pid>/exe

What binary is used when I run a command
which ls

What files is a process using
sudo lsof | grep apache2

What processes are listening for connections from the network
sudo lsof -i | grep LISTEN
sudo lsof -P -i :80

See network interfaces
ifconfig

See who is sending lots of traffic
sudo apt-get install nethogs
sudo nethogs enp0s3

Show resource consumption
top

Some sensitive places on Linux
/etc/passwd
/home/some-user/.ssh/
/usr/bin 
/proc



