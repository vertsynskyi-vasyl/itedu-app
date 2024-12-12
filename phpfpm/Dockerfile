# Dockerfile.phpfpm
FROM ubuntu:24.04

# Update and install PHP and necessary extensions
RUN apt-get update && apt-get install -y \
    php \
    php-cli \
    php-mysql \
    php-gd \
    php-xml \
    php-fpm && \
    apt-get clean

# Create the wordpress_user and group
RUN groupadd wordpress_user && \
    useradd -g wordpress_user wordpress_user

# Add PHP-FPM pool configuration
COPY wordpress_pool.conf /etc/php/8.3/fpm/pool.d/wordpress_pool.conf

# Add phpinfo test file
RUN mkdir -p /var/www/wp.itedu.work.gd && \
    echo "<?php phpinfo(); ?>" > /var/www/wp.itedu.work.gd/info.php

# Ensure the correct ownership of the web directory
RUN chown -R wordpress_user:wordpress_user /var/www/wp.itedu.work.gd
RUN touch /var/log/php8.3-fpm.log && \
    chown -R wordpress_user:wordpress_user /var/log/php8.3-fpm.log

# Expose port 9000
EXPOSE 9000

# Expose PHP-FPM socket
CMD ["php-fpm8.3", "-F"]

