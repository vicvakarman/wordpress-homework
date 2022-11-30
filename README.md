# VPS Configuring
### Picking OS for VPS
As OS for my VPS I chose Debian 11 *bullseye*. The reason for that is because it's new Long Term Supported version of Debian, which will be [supported](https://www.debian.org/News/2021/20210814) for the next 5 years. It is a massive community-run distro, no company can claim to be owning the Debian, or steering the project’s direction. The attraction of a large number of people to it is also due to its free software culture. There is a particular gap of almost three years between the releases of Debian versions. This helps to avoid the software breaking due to switching the performances of the system.
#### Why Debian and not Ubuntu?
First of all, I have used it more, then ubuntu, personally. It's more lightweight (it comes with almost no bundled or pre-packed software and features). More configurable. Ubuntu is for normal user, more user friendly (developer doesn't need this), etc.

### Installing OS
**Normal install**

![Capture1](https://user-images.githubusercontent.com/118899872/204775788-2450e4b7-211f-467e-a384-dc62f52e9a4a.PNG)

#### Choose language
**English**

![Capture2](https://user-images.githubusercontent.com/118899872/204775877-b70c1334-a493-49e3-9ec2-fcea6593e8e2.PNG)

#### Select location
```
other - Europe - Czechia
```

![Capture3](https://user-images.githubusercontent.com/118899872/204775942-ca02d96c-9d1a-4906-bb82-938815ef5fa1.PNG)

#### Configure locales
**en_US.UTF-8**

![Capture4](https://user-images.githubusercontent.com/118899872/204775966-5cd83baf-70f7-48bb-b3dd-88d2ecf45cd2.PNG)

#### Configure the keyboard
**American English**

![Capture5](https://user-images.githubusercontent.com/118899872/204776032-8342abd1-8308-4bec-834b-1dddafba774b.PNG)

#### Configure the network
**manually**

![Capture6](https://user-images.githubusercontent.com/118899872/204776320-f54ab3fe-2db7-44c1-bf05-a3f575c41373.PNG)

**ip address**

![Capture7](https://user-images.githubusercontent.com/118899872/204776369-788af55d-8ddf-4470-b3b0-0fc2e168543f.PNG)

**netmask**

![Capture8](https://user-images.githubusercontent.com/118899872/204776391-0ee5c15f-5926-4670-a37f-85a58c592797.PNG)

**gateway**

![Capture9](https://user-images.githubusercontent.com/118899872/204776408-9fa86605-5533-4275-b919-e83a43a9e517.PNG)

**nameservers**

![Capture10](https://user-images.githubusercontent.com/118899872/204776437-b9129b08-e3a1-473c-9fb5-3e689561c5de.PNG)

**hostname**

![Capture11](https://user-images.githubusercontent.com/118899872/204776464-d7370262-d58e-4ff5-ac99-7a4e704f7834.PNG)

**domain name (nothing)**

![Capture12](https://user-images.githubusercontent.com/118899872/204776491-bef14e86-d735-4111-baa6-a0ea7b4f84fc.PNG)


#### Set up users and passwords
**root password**

![Capture13](https://user-images.githubusercontent.com/118899872/204776698-d78323b6-4284-4183-b89e-c0dfc041af23.PNG)

**verify**

![Capture14](https://user-images.githubusercontent.com/118899872/204776729-b7599604-1c08-4aea-acaf-45ec7318e457.PNG)

**new user name**

![Capture15](https://user-images.githubusercontent.com/118899872/204776755-78e7e13d-9da3-41a6-a003-00016dae227a.PNG)

**user name account**

![Capture16](https://user-images.githubusercontent.com/118899872/204776777-39c6c280-f117-4498-97a7-30c8e6a7229f.PNG)

**user password**

![Capture17](https://user-images.githubusercontent.com/118899872/204776809-2dc0ee3f-fb77-4712-b128-f92da67b1cda.PNG)

**user password verify**

![Capture18](https://user-images.githubusercontent.com/118899872/204776816-5373d837-4766-45c4-aa9d-3aec11fe1039.PNG)


#### Disk partitions
**manual**

![Capture19](https://user-images.githubusercontent.com/118899872/204776866-3d82ca82-82f2-475a-92b8-471c6518be03.PNG)

```
PARTITION	SIZE	                    USAGE
/            4 GB	                    System files / all files
/boot  	  256 MB         	         Boot files
/home  	  100 MB	                  User files
/tmp  	   50 MB	                   Temporal files
/usr  	   2 GB	                    Program files
/var  	   400 MB	                  Dynamic data
/var/log     1GB                         Logs
```

![Capture20](https://user-images.githubusercontent.com/118899872/204777072-5032f176-d0c4-4f3a-84f6-e26b737ed4a2.PNG)
![Capture21](https://user-images.githubusercontent.com/118899872/204777078-3d930e02-89b9-4fff-bd01-317ed097ed28.PNG)

**/boot**

![Capture22](https://user-images.githubusercontent.com/118899872/204777101-99dc3665-3568-4797-8ab7-9a2b48f2c0eb.PNG)

We can add swap memory, but for our now goals now it is unnecessary.

**LVM group**

![Capture23](https://user-images.githubusercontent.com/118899872/204777138-6b710e3a-7d6b-4bef-8513-c962077eed45.PNG)
![Capture24](https://user-images.githubusercontent.com/118899872/204777214-90654c77-0d8f-468a-93c6-e207844cecd5.PNG)
![Capture25](https://user-images.githubusercontent.com/118899872/204777229-5c74a08b-b23a-493c-ba51-39d9191877b3.PNG)
![Capture26](https://user-images.githubusercontent.com/118899872/204777247-d5d0513c-5f99-486b-8bc5-119d9b69989a.PNG)
![Capture27](https://user-images.githubusercontent.com/118899872/204777264-8c043a05-483f-4aeb-bb47-58ba9cd575f6.PNG)

**create logical volumes**

![Capture28](https://user-images.githubusercontent.com/118899872/204777574-05eeda4e-4fad-4ccd-831e-ec54958bbf3f.PNG)
![Capture29](https://user-images.githubusercontent.com/118899872/204777592-ca85da41-b61b-4797-a6a3-6436bee0ebd5.PNG)

**configure created lv partitions as /boot before**

![Capture31](https://user-images.githubusercontent.com/118899872/204777666-d2f6d4dd-88c1-4b4d-bcdf-18d7d7b816b0.PNG)

**finish and write**

![Capture32](https://user-images.githubusercontent.com/118899872/204778566-4f4cd567-8c30-4e75-b616-33e058a5b22e.PNG)

![Capture33](https://user-images.githubusercontent.com/118899872/204778720-3e7f853e-633c-40d5-94f9-2f9566c0d8b1.PNG)

#### Package manager
**Czechia**

![Capture34](https://user-images.githubusercontent.com/118899872/204778835-cf999cce-83a4-45ca-a92b-939c16a083e5.PNG)

**ftp.cz.debian.org**

![Capture35](https://user-images.githubusercontent.com/118899872/204778847-61789ca0-7cb7-45d8-b3d5-fdaa365d1b95.PNG)

#### Proxy
**none**

![Capture36](https://user-images.githubusercontent.com/118899872/204779007-2703a7b0-e250-40c5-ac69-1919d63d9e4c.PNG)

#### Software selection
**just *continue***

![Capture37](https://user-images.githubusercontent.com/118899872/204779061-13fdbae6-9490-42df-9652-c08ff3a81a0d.PNG)

#### Grub
**Yes**

![Capture38](https://user-images.githubusercontent.com/118899872/204779112-611f084f-b11d-4f85-8553-7d6c24e31bdb.PNG)

The remove the installation media and reboot VPS.

### Configure user and ssh
Before every configuration we have to check packages' updates.
```
apt update & upgrade
```
Then we will install the sudo - allows a system administrator to delegate authority to give certain users. And grant admin prevelegies to our created user.
```
apt-get install sudo -y
usermod -aG sudo klient1015
```
Check.
```
id klient1015
```

Now we will go to shh configurations. Don't forget to do a backup.
```
cd /etc/ssh/
cp sshd_config sshd_config_backup
nano sshd_config
```
Change port from 22 to some port, 35737 in my case, to prevent for example brutforce attacks!

You can take ake port that is not from list https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers.
Next we will permit the root login through ssh for better defense.
```
PermitRootLogin yes
```
We can use the PubkeyAuthentication but we will do it later.

### Installing LAMP stack

#### Apache
Install Apache and make user www-date as owner of /www/ directory + change access rights.
```
-rw-r--r-- 12 linuxize users 12.0K Apr  28 10:10 file_name
|[-][-][-]-   [------] [---]
| |  |  | |      |       |
| |  |  | |      |       +-----------> 7. Group
| |  |  | |      +-------------------> 6. Owner
| |  |  | +--------------------------> 5. Alternate Access Method
| |  |  +----------------------------> 4. Others Permissions
| |  +-------------------------------> 3. Group Permissions
| +----------------------------------> 2. Owner Permissions
+------------------------------------> 1. File Type
```

```
sudo apt install apache2
chown -R www-data:www-data /var/www/ && chmod -R 755 /var/www/
```

#### Firewall
First of all we will install the iptables, I don't want to use ufw cause with iptables I feel more control, what I am doing.
Then create test rules file.
```
apt install iptables
touch /etc/iptables.test.rules
```

You can paste mine rules here, or write yours. All rules are commented.
```
*filter

# Allows all loopback (lo0) traffic and drop all traffic to 127/8 that doesn't use lo0
-A INPUT -i lo -j ACCEPT
-A INPUT ! -i lo -d 127.0.0.0/8 -j REJECT

# Accepts all established inbound connections
-A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Allows all outbound traffic
# You could modify this to only allow certain traffic
-A OUTPUT -j ACCEPT

# Allows HTTP and HTTPS connections from anywhere (the normal ports for websites)
-A INPUT -p tcp --dport 80 -j ACCEPT
-A INPUT -p tcp --dport 443 -j ACCEPT

# Allows SSH connections
# The --dport number is the same as in /etc/ssh/sshd_config
-A INPUT -p tcp -m state --state NEW --dport 35737 -j ACCEPT

# It's better to have ssh access from local network, for example if there
# is VPN in same local network, firstly we connect to VPN and then we are
# allowed to connect to our server.
# Or we allow to connect from certain IP (our home ip / external VPN
# service)

# Allow ping
#  note that blocking other types of icmp packets is considered a bad idea by some
#  remove -m icmp --icmp-type 8 from this line to allow all kinds of icmp:
-A INPUT -p icmp -m icmp --icmp-type 8 -j ACCEPT

# log iptables denied calls (access via 'dmesg' command)
-A INPUT -m limit --limit 5/min -j LOG --log-prefix "iptables denied: " --log-level 7

# Reject all other inbound - default deny unless explicitly allowed policy:
-A INPUT -j DROP
-A FORWARD -j DROP

COMMIT
```

Activate and save.

```
iptables-restore < /etc/iptables.test.rules
iptables -L
iptables-save > /etc/iptables.up.rules
```

Make sure they will restored after reboot.

```
nano /etc/network/if-pre-up.d/iptables
```
Paste this configuration (command).

```
#!/bin/sh
/sbin/iptables-restore < /etc/iptables.up.rules
```

Make executable.
```
chmod +x /etc/network/if-pre-up.d/iptables
```

#### MariaDB
Firstly please install. On debian there is not MySQL, but is MariaDB - relational database management system. 
```
sudo apt install mariadb-server
sudo mysql_secure_installation
```

Questions during secure installation.
```
"Just press enter, cause there is no root password."

"n"
"Y"
"New maridb root user password."
"Y"
"Y"
"Y"
"Y"
```

Create new database and user for wordpress.
```
CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
GRANT ALL ON wordpress.* TO 'wp'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
FLUSH PRIVILEGES;
exit;
```

Checking.
```
mariadb -u wp -p

SHOW DATABASES;
exit;
```

#### PHP
So we won't install the normal php, we willuse the php-fpm - https://php-fpm.org/ . basically to have better performance, as we will be using wordpress.
Firstly we add newest packeges for php and then install. We will also install some extra packages for php, which are mostly used (mainly by wordpress itself).
```
apt-get install ca-certificates apt-transport-https software-properties-common wget curl lsb-release -y
curl -sSL https://packages.sury.org/php/README.txt | sudo bash -x
apt udpate
apt upgrade
apt install php8.1-fpm libapache2-mod-fcgid -y
apt install php8.1-common php8.1-mysql php8.1-xml php8.1-xmlrpc php8.1-curl php8.1-gd php8.1-imagick php8.1-cli php8.1-dev php8.1-imap php8.1-mbstring php8.1-soap php8.1-zip php8.1-bcmath -y
```
Sed command is used for changing values without opening the file itself.
After installation we will activate all. End restart few times.
```
sed -i 's/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g' /etc/php/8.1/fpm/php.ini

sudo systemctl restart php8.1-fpm


sudo a2enmod proxy_fcgi setenvif
sudo systemctl restart apache2
sudo a2enconf php8.1-fpm
sudo systemctl restart apache2
sudo systemctl status php8.1-fpm
php --version
```

Php configuration for wordpress.
```
sed -i 's/memory_limit = 128M/memory_limit = 512M/g' /etc/php/8.1/fpm/php.ini
sed -i 's/post_max_size = 8M/post_max_size = 128M/g' /etc/php/8.1/fpm/php.ini
sed -i 's/max_file_uploads = 20/max_file_uploads = 30/g' /etc/php/8.1/fpm/php.ini
sed -i 's/max_execution_time = 30/max_execution_time = 900/g' /etc/php/8.1/fpm/php.ini
sed -i 's/max_input_time = 60/max_input_time = 3000/g' /etc/php/8.1/fpm/php.ini
sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 128M/g' /etc/php/8.1/fpm/php.ini
sudo systemctl restart php8.1-fpm
```

#### Wordpress
```
sudo nano /etc/apache2/mods-enabled/dir.conf
```
bring *index.php* to the front

```
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
Restart.
```
sudo systemctl restart apache2
```

Copy configuration.
```
cp 000-default.conf wordpress.conf
```

Add block so we can use .httaccess file.
```
<Directory /var/www/wordpress/>
	AllowOverride All
</Directory>
```

Check config.
```
sudo a2enmod rewrite
sudo apache2ctl configtest
sudo systemctl restart apache2
```

Enable configuration (remove the default one).
```
cd /etc/apache2/sites-enabled
rm 000-default.conf
sudo a2ensite wordpress.conf
sudo systemctl reload apache2
```

Install wordpress files.
```
cd /tmp
curl -O https://wordpress.org/latest.tar.gz
tar xzvf latest.tar.gz --directory /var/www/wordpress
touch /var/www/wordpress/.htaccess
cp /var/www/wordpress/wp-config-sample.php /var/www/wordpress/wp-config.php
mkdir /var/www/wordpress/wp-content/upgrade
```

Configuring access and wordpress config.
```
chown -R www-data:www-data /var/www/wordpress
sudo find /var/www/wordpress/ -type d -exec chmod 750 {} \;
sudo find /var/www/wordpress/ -type f -exec chmod 640 {} \;

curl -s https://api.wordpress.org/secret-key/1.1/salt/
nano /var/www/wordpress/wp-config.php
```
*paste values*

Configure database access in wordpress config
```
nano /var/www/wordpress/wp-config.php
```
```
. . .

define('DB_NAME', 'wordpress');

/** MySQL database username */
define('DB_USER', 'wp');

/** MySQL database password */
define('DB_PASSWORD', 'password');

. . .

define('FS_METHOD', 'direct');
```

Complete instalation through web interface.

![Capture39](https://user-images.githubusercontent.com/118899872/204786294-e75975a8-e0f1-4ba1-8235-0b0c8ef3e48a.PNG)
![Capture40](https://user-images.githubusercontent.com/118899872/204786314-7d5bc141-6f15-4d66-98fd-5406afada7e1.PNG)

