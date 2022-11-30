# VPS Configuring
### Picking OS for VPS
As OS for my VPS I chose Debian 11 *bullseye*. The reason for that is because it's new Long Term Supported version of Debian, which will be [supported](https://www.debian.org/News/2021/20210814) for the next 5 years. It is a massive community-run distro, no company can claim to be owning the Debian, or steering the project’s direction. The attraction of a large number of people to it is also due to its free software culture. There is a particular gap of almost three years between the releases of Debian versions. This helps to avoid the software breaking due to switching the performances of the system.
#### Why Debian and not Ubuntu?
First of all, I have used it more, then ubuntu, personally. It's more lightweight (it comes with almost no bundled or pre-packed software and features). More configurable. Ubuntu is for normal user, more user friendly (developer doesn't need this), etc.

### Installing OS
#### Choose language
(English.)

#### Select location
```
other - Europe - Czechia
```

#### Configure locales
(en_US.UTF-8)

#### Configure the keyboard
(American English)

#### Configure the network
(manually)
(ip address)
(netmask)
(gateway)
(nameservers)
(hostname)
(domain name (nothing))

#### Set up users and passwords
(root password)
(verify)
(new user name)
(user name account)
(user password)
(user password verify)

#### Disk partitions
(manual)
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
(/boot)
(we can add swap memory, but for our now goals it is unnecessary)
(LVM group)
(configure created lv partitions)
(finish)
(write)

#### Package manager
(Czechia)
(ftp.cz.debian.org)

#### Proxy
(none)

#### Software selection
(just *continue*)

#### Grub
(Yes)

The remove the installation media and reboot VPS.

### Configure user and ssh
```
apt update & upgrade

apt-get install sudo -y
usermod -aG sudo klient1015
id klient1015
```

```
cd /etc/ssh/
cp sshd_config sshd_config_backup
nano sshd_config
```
change port from 22 to some port, 35737 in my case, to prevent for example brutforce attacks

take port that is not from list https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers

```
PermitRootLogin yes
```
we can use the PubkeyAuthentication but we will do it later

### Installing LAMP stack

#### Apache
Install Apache using Debian’s package manager, APT:

```
sudo apt install apache2
chown -R www-data:www-data /var/www/ && chmod -R 755 /var/www/
```

#### Firewall
```
apt install iptables
touch /etc/iptables.test.rules
```

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

activate and save

```
iptables-restore < /etc/iptables.test.rules
iptables -L
iptables-save > /etc/iptables.up.rules
```

make sure they will restored after reboot

```
nano /etc/network/if-pre-up.d/iptables
```
paste this

```
#!/bin/sh
/sbin/iptables-restore < /etc/iptables.up.rules
```

make executable
```
chmod +x /etc/network/if-pre-up.d/iptables
```

#### MariaDB
install
```
sudo apt install mariadb-server
sudo mysql_secure_installation
```

questions
```
"just press enter, cause there is no root password"

"n"
"Y"
"new maridb root user password"
"Y"
"Y"
"Y"
"Y"
```

create new database and user for wordpress
```
CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
GRANT ALL ON wordpress.* TO 'wp'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
FLUSH PRIVILEGES;
exit;
```

checking
```
mariadb -u wp -p

SHOW DATABASES;
exit;
```

#### PHP
installation
```
apt-get install ca-certificates apt-transport-https software-properties-common wget curl lsb-release -y
curl -sSL https://packages.sury.org/php/README.txt | sudo bash -x
apt udpate
apt upgrade
apt install php8.1-fpm libapache2-mod-fcgid -y
apt install php8.1-common php8.1-mysql php8.1-xml php8.1-xmlrpc php8.1-curl php8.1-gd php8.1-imagick php8.1-cli php8.1-dev php8.1-imap php8.1-mbstring php8.1-soap php8.1-zip php8.1-bcmath -y

sed -i 's/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/g' /etc/php/8.1/fpm/php.ini

sudo systemctl restart php8.1-fpm


sudo a2enmod proxy_fcgi setenvif
sudo systemctl restart apache2
sudo a2enconf php8.1-fpm
sudo systemctl restart apache2
sudo systemctl status php8.1-fpm
php --version
```

php configuration
```
sed -i 's/memory_limit = 128M/memory_limit = 512M/g' /etc/php/8.1/fpm/php.ini
sed -i 's/post_max_size = 8M/post_max_size = 128M/g' /etc/php/8.1/fpm/php.ini
sed -i 's/max_file_uploads = 20/max_file_uploads = 30/g' /etc/php/8.1/fpm/php.ini
sed -i 's/max_execution_time = 30/max_execution_time = 900/g' /etc/php/8.1/fpm/php.ini
sed -i 's/max_input_time = 60/max_input_time = 3000/g' /etc/php/8.1/fpm/php.ini
sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 128M/g' /etc/php/8.1/fpm/php.ini
sudo systemctl restart php8.1-fpm
```

#### wordpress
```
sudo nano /etc/apache2/mods-enabled/dir.conf
```
bring *index.php* to the front

```
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

```
sudo systemctl restart apache2
```

configuring
```
cp 000-default.conf wordpress.conf
```

add block
```
<Directory /var/www/wordpress/>
	AllowOverride All
</Directory>
```

```
sudo a2enmod rewrite
sudo apache2ctl configtest
sudo systemctl restart apache2
```

enable configuration
```
cd /etc/apache2/sites-enabled
rm 000-default.conf
sudo a2ensite wordpress.conf
sudo systemctl reload apache2
```

install wordpress files
```
cd /tmp
curl -O https://wordpress.org/latest.tar.gz
tar xzvf latest.tar.gz --directory /var/www/wordpress
touch /var/www/wordpress/.htaccess
cp /var/www/wordpress/wp-config-sample.php /var/www/wordpress/wp-config.php
mkdir /var/www/wordpress/wp-content/upgrade
```

configuring
```
chown -R www-data:www-data /var/www/wordpress
sudo find /var/www/wordpress/ -type d -exec chmod 750 {} \;
sudo find /var/www/wordpress/ -type f -exec chmod 640 {} \;

curl -s https://api.wordpress.org/secret-key/1.1/salt/
nano /var/www/wordpress/wp-config.php
```
*paste values*

configure database
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

complete instalation through web interface
