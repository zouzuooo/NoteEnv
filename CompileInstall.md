CentOS

# 创建用户组
groupadd www
# 创建用户
useradd -g www www -M -s /sbin/nologin
-g www 指定用户组
-M 不创建家目录（程序运行不需要家目录）
-s /sbin/nologin 不允许登录，更加安全


tar -xf archive.tar.gz

---------------
磁盘挂载和格式化 : https://zhuanlan.zhihu.com/p/145773155

fdisk -l
sudo fdisk /dev/xvdb 
n
1


w

fdisk -l:  查看到以下信息表示分区完成, 可以挂载目录了
Device     Boot Start      End  Sectors Size Id Type
/dev/xvdb1       2048 41943039 41940992  20G 83 Linux

//格式化分区
sudo mkfs.ext4 /dev/xvdb1

//创建准备挂载的目录
sudo mkdir /www

mount /dev/xvdb1 /www

//设置开机自动挂载
echo /dev/xvdb1 /www ext4 defaults 0 0 >> /etc/fstab

------------查看网络端口
ss -tuln
netstat -ntlp 
------------------

yum install -y redis
yum install -y nginx

//查看已安装的包
yum list installed | grep package


//根据官网安装依赖
sudo yum install -y autoconf automake libtool re2c

wget https://www.php.net/distributions/php-8.1.22.tar.gz

./configure --help

  --with-avif             GD: Enable AVIF support (only for bundled libgd)    
  --with-webp             GD: Enable WEBP support (only for bundled libgd)
  --with-jpeg             GD: Enable JPEG support (only for bundled libgd)
  --with-xpm              GD: Enable XPM support (only for bundled libgd)
  --with-freetype         GD: Enable FreeType 2 support (only for bundled

--with-avif  需要 libavif, Aws默认源没有,  先跳过
--with-xpm  https://en.wikipedia.org/wiki/X_PixMap

./configure --prefix=/www/server/php8.1 --enable-fpm --enable-bcmath --with-curl --enable-pcntl  --with-pdo-mysql --with-zip --with-bz2 --enable-mbstring --enable-gd --with-webp --with-jpeg  --with-freetype

反复执行  yum search... yum install ...  直到 configure 通过..

// 2023-08-10 整理
sudo yum install -y autoconf automake libtool re2c libxml2 libxml2-devel sqlite-devel bzip2 bzip2-devel libcurl libcurl-devel libpng libpng-devel libwebp libwebp-devel libjpeg-turbo libjpeg-turbo-devel freetype freetype-devel libXpm libXpm-devel oniguruma oniguruma-devel libzip libzip-devel


make & make install


php-redis 需要后续单独安装:

### PHP 其他参考-------------------------


#For Php8.1
sudo yum install libxml2 libxml2-devel libsqlite3x-devel openssl bzip2 libcurl-devel libcurl libjpeg libpng freetype gmp libmcrypt libmcrypt-devel readline readline-devel libxslt libxslt-devel zlib zlib-devel glibc glib2 ncurses curl gdbm-devel db4-devel libXpm-devel libX11-devel gd-devel gmp-devel expat-devel xmlrpc-c xmlrpc-c-devel libicu-devel libmcrypt-devel libmemcached-devel -y



./configure --prefix=/www/server/php81 --with-config-file-path=/www/server/php81/etc --enable-fpm --with-fpm-group=www --enable-mysqlnd --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-iconv-dir --with-freetype --with-mcrypt --with-jpeg --with-png -with-zlib --with-libxml-dir --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl -enable-mbstring --enable-gd --with-openssl --with-mhash --enable-pcntl --with-xmlrpc --enable-zip --enable-soap --with-gettext --enable-opcache --with-xsl --enable-sockets --enable-mbregex --enable-ftp --with-webp

//参考
sudo apt install php8.1 php8.1-bcmath php8.1-dev php8.1-gd php8.1-fpm php8.1-iconv php8.1-curl php8.1-pdo php8.1-pdo-mysql php8.1-pdo-sqlite php8.1-phar php8.1-redis php8.1-zip php8.1-bz2 php8.1-mbstring

### PM2 

### For Mysql8
sudo yum -y install gcc gcc-c++ cmake ncurses-devel bison openssl-devel rpcgen


关于mysql直接参考官网提供的 yum方式安装
https://dev.mysql.com/doc/mysql-yum-repo-quick-guide/en/#repo-qg-yum-installing

systemctl start mysqld
systemctl status mysqld
systemctl stop mysqld

2023-08-10T12:46:18.991330Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: 1*C6BwjfOZKR
ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';

变更默认存放目录: https://blog.51cto.com/u_15350046/3708113
mysql> show variables like '%dir%';
+-----------------------------------------+--------------------------------+
| Variable_name                           | Value                          |
+-----------------------------------------+--------------------------------+
| basedir                                 | /usr/                          |
| binlog_direct_non_transactional_updates | OFF                            |
| character_sets_dir                      | /usr/share/mysql-8.0/charsets/ |
| datadir                                 | /var/lib/mysql/                |
| innodb_data_home_dir                    |                                |
| innodb_directories                      |                                |
| innodb_doublewrite_dir                  |                                |
| innodb_log_group_home_dir               | ./                             |
| innodb_max_dirty_pages_pct              | 90.000000                      |
| innodb_max_dirty_pages_pct_lwm          | 10.000000                      |
| innodb_redo_log_archive_dirs            |                                |
| innodb_temp_tablespaces_dir             | ./#innodb_temp/                |
| innodb_tmpdir                           |                                |
| innodb_undo_directory                   | ./                             |
| lc_messages_dir                         | /usr/share/mysql-8.0/          |
| plugin_dir                              | /usr/lib64/mysql/plugin/       |
| replica_load_tmpdir                     | /tmp                           |
| slave_load_tmpdir                       | /tmp                           |
| tmpdir                                  | /tmp                           |
+-----------------------------------------+--------------------------------+
systemctl stop mysqld
cp -R /var/lib/mysql /www/mysql_data/
chown mysql:mysql -R /www/mysql_data
vim /etc/my.cnf


wget https://downloads.mysql.com/archives/get/p/23/file/mysql-8.0.33-linux-glibc2.28-x86_64.tar.gz




//无奈 Aws 免费机器无法完成Php编辑安装, 先用自带软件源试一下   可以接受, 常用扩展都有, 且支持pecl 
php8.1.x86_64 : PHP scripting language for creating dynamic web sites
============================================================================================================ Name Matched: php8.1 ============================================================================================================
php8.1-bcmath.x86_64 : A module for PHP 8.1 applications for using the bcmath library
php8.1-cli.x86_64 : Command-line interface for PHP 8.1
php8.1-common.x86_64 : Common files for PHP 8.1
php8.1-dba.x86_64 : A database abstraction layer module for PHP 8.1 applications
php8.1-dbg.x86_64 : The interactive PHP 8.1 debugger
php8.1-devel.x86_64 : Files needed for building PHP 8.1 extensions
php8.1-embedded.x86_64 : PHP 8.1 library for embedding in applications
php8.1-enchant.x86_64 : Enchant spelling extension for PHP 8.1 applications
php8.1-ffi.x86_64 : Foreign Function Interface
php8.1-fpm.x86_64 : PHP 8.1 FastCGI Process Manager
php8.1-gd.x86_64 : A module for PHP 8.1 applications for using the gd graphics library
php8.1-gmp.x86_64 : A module for PHP 8.1 applications for using the GNU MP library
php8.1-intl.x86_64 : Internationalization extension for PHP 8.1 applications
php8.1-ldap.x86_64 : A module for PHP 8.1 applications that use LDAP
php8.1-mbstring.x86_64 : A module for PHP 8.1 applications which need multi-byte string handling
php8.1-mysqlnd.x86_64 : A module for PHP 8.1 applications that use MySQL databases
php8.1-odbc.x86_64 : A module for PHP 8.1 applications that use ODBC databases
php8.1-opcache.x86_64 : The Zend OPcache
php8.1-pdo.x86_64 : A database access abstraction module for PHP 8.1 applications
php8.1-pgsql.x86_64 : A PostgreSQL database module for PHP 8.1
php8.1-process.x86_64 : Modules for PHP 8.1 script using system process interfaces
php8.1-pspell.x86_64 : A module for PHP 8.1 applications for using pspell interfaces
php8.1-snmp.x86_64 : A module for PHP 8.1 applications that query SNMP-managed devices
php8.1-soap.x86_64 : A module for PHP 8.1 applications that use the SOAP protocol
php8.1-tidy.x86_64 : Standard PHP 8.1 module provides tidy library support
php8.1-xml.x86_64 : A module for PHP 8.1 applications which use XML

sudo yum install -y php8.1 php8.1-bcmath php8.1-cli php8.1-common php8.1-devel php8.1-fpm php8.1-gd php8.1-intl php8.1-mbstring php8.1-mysqlnd php8.1-pdo php8.1-xml 

[ec2-user@ip-172-31-42-54 ~]$ php -m
[PHP Modules]
bcmath
bz2
calendar
Core
ctype
curl
date
dom
exif
fileinfo
filter
ftp
gd
gettext
hash
iconv
intl
json
libxml
mbstring
mysqli
mysqlnd
openssl
pcntl
pcre
PDO
pdo_mysql
pdo_sqlite
Phar
posix
readline
Reflection
session
shmop
SimpleXML
sockets
SPL
sqlite3
standard
sysvmsg
sysvsem
sysvshm
tokenizer
xml
xmlreader
xmlwriter
xsl
Zend OPcache
zlib

[Zend Modules]
Zend OPcache


/run/php-fpm/www.sock

安装: sudo pecl install redis


sudo yum install -y nodejs nodejs-devel
sudo npm i -g pm2


 rsync -avL --progress -e 'ssh -i ~/.ssh/mana.pem' /home/micoing/Documents/Compiled/mwback/Workspace/code.tar.gz ec2-user@3.25.227.213:/www/web/tmpdir/

 rsync -avL --progress -e 'ssh -i ~/.ssh/mana.pem' /home/micoing/Downloads/phpMyAdmin-5.2.1-all-languages.zip ec2-user@3.25.227.213:/www/web/tmpdir/