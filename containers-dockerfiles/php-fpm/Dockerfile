FROM php:7.2.12-fpm-stretch
RUN apt-get -y update && apt-get -y --no-install-recommends upgrade && \
pecl install xdebug && docker-php-ext-enable xdebug && \
touch /xdebug.log && chmod 777 /xdebug.log && \
XDEBUG_INI=$(find / -name docker-php-ext-xdebug.ini) && \
echo "xdebug.remote_enable=on" >> $XDEBUG_INI && \
echo "xdebug.remote_handler=dbgp" >> $XDEBUG_INI && \
echo "xdebug.remote_port=9000" >> $XDEBUG_INI && \
echo "xdebug.remote_autostart=1" >> $XDEBUG_INI && \
echo "xdebug.idekey=\"PHPSTORM\"" >> $XDEBUG_INI && \
echo "xdebug.remote_host=\"172.19.0.1\"" >> $XDEBUG_INI && \
echo "xdebug.remote_log=/xdebug.log" >> $XDEBUG_INI && \
apt-get install -y libxml2-dev libzip-dev git libpng-dev libjpeg-dev libfreetype6-dev libssl-dev && \
docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ && \
docker-php-ext-install pcntl pdo mysqli pdo_mysql session simplexml sockets zip gd json && \
chmod 777 /var/www && \
usermod -u 1001 www-data && \
mkdir -p /var/tmp/composer && \
curl -o /var/tmp/composer/composer-setup.php https://getcomposer.org/installer && \
SHA=$(sha384sum /var/tmp/composer/composer-setup.php | awk '{ print $1; }') && \
if [ $SHA = "48e3236262b34d30969dca3c37281b3b4bbe3221bda826ac6a9a62d6444cdb0dcd0615698a5cbe587c3f0fe57a54d8f5" ]; then cd /var/tmp/composer && php /var/tmp/composer/composer-setup.php; else echo 'duypa!!!'; fi && \
rm /var/tmp/composer/composer-setup.php