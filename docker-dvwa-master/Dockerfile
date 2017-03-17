FROM tutum/lamp

MAINTAINER Daniel Romero <infoslack@gmail.com>

ENV VERSION 1.9

RUN rm -rf /app && \
    apt-get update && \
    apt-get install -y wget php5-gd && \
    rm -rf /var/lib/apt/lists/*

COPY conf/* /tmp/

RUN wget https://github.com/ethicalhack3r/DVWA/archive/v${VERSION}.tar.gz && \
    tar xvf /v${VERSION}.tar.gz && \
    mv -f /DVWA-${VERSION} /app && \
    rm /app/.htaccess && \
    mv /tmp/.htaccess /app && \
    chmod -R 777 /app/hackable/uploads /app/external/phpids/0.6/lib/IDS/tmp/phpids_log.txt && \
    sed -i 's/allow_url_include = Off/allow_url_include = On/g' /etc/php5/apache2/php.ini && \
    sed -i "s/$_DVWA[ 'recaptcha_private_key' ] = ''/$_DVWA[ 'recaptcha_private_key' ] = 'TaQ185RFuWM'/g" /app/config/config.inc.php && \
    sed -i "s/$_DVWA[ 'recaptcha_public_key' ] = ''/$_DVWA[ 'recaptcha_public_key' ] = 'TaQ185RFuWM'/g" /app/config/config.inc.php && \
    sed -i 's/FileInfo/All/g' /etc/apache2/sites-available/000-default.conf && \
    sed -i 's/root/admin/g' /app/config/config.inc.php && \
    echo "sed -i \"s/p@ssw0rd/\$PASS/g\" /app/config/config.inc.php" >> /create_mysql_admin_user.sh && \
    echo 'session.save_path = "/tmp"' >> /etc/php5/apache2/php.ini


EXPOSE 80 3306

CMD ["/run.sh"]
