FROM php:8.1-apache
# Cài đặt các gói cần thiết và tiện ích mở rộng mysqli
RUN apt-get update && apt-get install -y \
    libmariadb-dev \
    && docker-php-ext-install mysqli \
    && docker-php-ext-enable mysqli
# Cấu hình Apache để phục vụ login.php
RUN echo "<Directory /var/www/html>\n    DirectoryIndex login.php\n</Directory>" > /etc/apache2/conf-available/custom.conf
RUN a2enconf custom
ENV APACHE_DOCUMENT_ROOT=/var/www/html
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
