#FROM wordpress:5.5.3-fpm-alpine
FROM wordpress:fpm-alpine
# PHP extensions
RUN set -ex \
  && apk --no-cache add \
  postgresql-dev autoconf gcc make g++ zlib-dev && \
  docker-php-ext-install pdo pdo_mysql pdo_pgsql && \
  pecl install -o -f redis && \
  rm -rf /tmp/pear && \
  docker-php-ext-enable redis && \
  apk del autoconf gcc make g++ zlib-dev

RUN touch /usr/local/etc/php/conf.d/memory-limit.ini && echo "memory_limit=512M" >> /usr/local/etc/php/conf.d/memory-limit.ini && \
    touch /usr/local/etc/php/conf.d/max-execution-time.ini && echo "max_execution_time=120" >> /usr/local/etc/php/conf.d/max-execution-time.ini && \
    sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 512M/g' /usr/local/etc/php/php.ini-production && \
    sed -i 's/post_max_size = 8M/post_max_size = 513M/g' /usr/local/etc/php/php.ini-production && \
    cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini && \
    sed -i "s/;env\[HOSTNAME\] = /env[HOSTNAME] = /" /usr/local/etc/php-fpm.d/www.conf && \
    sed -i "s/;env\[TMP\] = /env[TMP] = /" /usr/local/etc/php-fpm.d/www.conf && \
    sed -i "s/;env\[TMPDIR\] = /env[TMPDIR] = /" /usr/local/etc/php-fpm.d/www.conf && \
    sed -i "s/;env\[TEMP\] = /env[TEMP] = /" /usr/local/etc/php-fpm.d/www.conf && \
    sed -i "s/;env\[PATH\] = /env[PATH] = /" /usr/local/etc/php-fpm.d/www.conf && \
    sed -i "s/pm.max_children =.*/pm.max_children = 1200/" /usr/local/etc/php-fpm.d/www.conf && \
    sed -i "s/pm.start_servers =.*/pm.start_servers = 12/" /usr/local/etc/php-fpm.d/www.conf && \
    sed -i "s/pm.min_spare_servers =.*/pm.min_spare_servers = 6/" /usr/local/etc/php-fpm.d/www.conf && \
    sed -i "s/pm.max_spare_servers =.*/pm.max_spare_servers = 18/" /usr/local/etc/php-fpm.d/www.conf && \
    sed -i "s/;pm.max_requests =.*/pm.max_requests = 1000/" /usr/local/etc/php-fpm.d/www.conf

#RUN sed -i 's/128/4096/g' /usr/local/etc/php/conf.d/memory-limit.ini && \
 #   cat /usr/local/etc/php/conf.d/memory-limit.ini
