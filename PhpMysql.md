
sudo apt install mysql-client-8.0 mysql-server-8.0

mysql -u root
FLUSH PRIVILEGES;
ALTER USER 'root'@'localhost' IDENTIFIED BY '新密码';

sudo apt install php8.1 php8.1-bcmath php8.1-dev php8.1-gd php8.1-fpm php8.1-iconv php8.1-curl php8.1-pdo php8.1-pdo-mysql php8.1-pdo-sqlite php8.1-phar php8.1-redis php8.1-zip php8.1-bz2 php8.1-mbstring


//CentOS


npm install -g pm2



查看网络端口：
sudo lsof -i -P -n | grep LISTEN
sudo netstat -tuln


apt 安装后一般不需要配置服务。
sudo vim /etc/systemd/system/php-fpm8.1.service
    #[Unit]
    #Description=PHP FastCGI Process Manager
    #After=network.target
    #
    #[Service]
    #ExecStart=/usr/sbin/php-fpm8.1 --nodaemonize --fpm-config /etc/php/8.1/fpm/php-fpm.conf
    #ExecReload=/bin/kill -USR2 $MAINPID
    #ExecStop=/bin/kill -SIGINT $MAINPID
    #Type=notify
    #NotifyAccess=all
    #
    #[Install]
    #WantedBy=multi-user.target

sudo systemctl enable php-fpm8.1
sudo systemctl start php-fpm8.1


pm2...




--------------------
https://packagist.org/packages/haistar/shopee-php-sdk
composer require haistar/shopee-php-sdk