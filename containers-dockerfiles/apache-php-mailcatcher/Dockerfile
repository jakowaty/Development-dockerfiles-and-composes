FROM php:7.2.5-apache

RUN apt-get update -y && \
pecl install xdebug && docker-php-ext-enable xdebug && \
#touch /xdebug.log && chmod 777 /xdebug.log && \
XDEBUG_INI=$(find / -name docker-php-ext-xdebug.ini) && \
echo "xdebug.remote_enable=on" >> $XDEBUG_INI && \
echo "xdebug.remote_handler=dbgp" >> $XDEBUG_INI && \
echo "xdebug.remote_port=9000" >> $XDEBUG_INI && \
echo "xdebug.remote_autostart=1" >> $XDEBUG_INI && \
echo "xdebug.idekey=\"PHPSTORM\"" >> $XDEBUG_INI && \
echo "xdebug.remote_host=\"172.17.0.1\"" >> $XDEBUG_INI && \
#echo "xdebug.remote_log=/xdebug.log" >> $XDEBUG_INI && \
apt-get install -y libxml2-dev libzip-dev git libpng-dev libjpeg-dev libfreetype6-dev && \
docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
docker-php-ext-install pcntl pdo mysqli pdo_mysql session simplexml sockets zip gd && \
#mailcatcher
curl --location --output /usr/local/bin/mhsendmail https://github.com/mailhog/mhsendmail/releases/download/v0.2.0/mhsendmail_linux_amd64 && \
chmod +x /usr/local/bin/mhsendmail && \
touch /usr/local/etc/php/conf.d/php.ini && \
echo 'sendmail_path = "/usr/local/bin/mhsendmail --smtp-addr=mailer:1025 --from=no-reply@docker.dev"' >> /usr/local/etc/php/conf.d/php.ini && \
echo 'mail.log = "/var/log/php_mail.log"' >> /usr/local/etc/php/conf.d/php.ini && \
#use your current user UID
usermod -u 1001 www-data && \
a2enmod rewrite && \
service apache2 restart