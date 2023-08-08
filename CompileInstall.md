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

#For Php8.1
sudo yum install libxml2 libxml2-devel libsqlite3x-devel openssl bzip2 libcurl-devel libcurl libjpeg libpng freetype gmp libmcrypt libmcrypt-devel readline readline-devel libxslt libxslt-devel zlib zlib-devel glibc glib2 ncurses curl gdbm-devel db4-devel libXpm-devel libX11-devel gd-devel gmp-devel expat-devel xmlrpc-c xmlrpc-c-devel libicu-devel libmcrypt-devel libmemcached-devel -y


wget https://www.php.net/distributions/php-8.1.22.tar.gz


./configure --prefix=/www/server/php81 --with-config-file-path=/www/server/php81/etc --enable-fpm --with-fpm-group=www --enable-mysqlnd --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-iconv-dir --with-freetype --with-mcrypt --with-jpeg --with-png -with-zlib --with-libxml-dir --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem --enable-inline-optimization --with-curl -enable-mbstring --enable-gd --with-openssl --with-mhash --enable-pcntl --with-xmlrpc --enable-zip --enable-soap --with-gettext --enable-opcache --with-xsl --enable-sockets --enable-mbregex --enable-ftp --with-webp

//参考
sudo apt install php8.1 php8.1-bcmath php8.1-dev php8.1-gd php8.1-fpm php8.1-iconv php8.1-curl php8.1-pdo php8.1-pdo-mysql php8.1-pdo-sqlite php8.1-phar php8.1-redis php8.1-zip php8.1-bz2 php8.1-mbstring


#For Mysql8
sudo yum -y install gcc gcc-c++ cmake ncurses-devel bison openssl-devel rpcgen



wget https://downloads.mysql.com/archives/get/p/23/file/mysql-8.0.33-linux-glibc2.28-x86_64.tar.gz