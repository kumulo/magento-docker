FROM php:7.2-fpm

RUN apt-get update && apt-get install -y \
    git libmcrypt-dev libpq-dev \
    libcurl4-gnutls-dev libicu-dev \
    libvpx-dev libjpeg-dev libpng-dev \
    libxpm-dev zlib1g-dev libfreetype6-dev \
    libxml2-dev libexpat1-dev libbz2-dev \
    libgmp3-dev libldap2-dev unixodbc-dev \
    libsqlite3-dev libaspell-dev libsnmp-dev \
    libpcre3-dev libtidy-dev libsodium-dev libxslt1-dev

# Set timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install mbstring \
    pdo \
    pdo_mysql \
    bcmath \
    soap \
    xsl \
    curl \
    json \
    intl \
    xml \
    zip \
    bz2 \
    exif \
    sodium

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --enable-exif
RUN docker-php-ext-install -j$(nproc) gd

RUN pear upgrade pear
RUN pear channel-discover pear.symfony-project.com
RUN pear install PHP_CodeSniffer

RUN pecl install xdebug
RUN docker-php-ext-enable xdebug

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Install Node, Yarn
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs
RUN npm install -g yarn

WORKDIR /var/www/magento

#magento setup:install --base-url=http://localhost:82/ \
	--db-host=mysql --db-name=magento \
	--db-user=root --db-password=passwd \
	--admin-firstname=Magento --admin-lastname=User --admin-email=user@example.com \
	--admin-user=admin --admin-password=admin123 --language=fr_FR \
	--currency=EUR --timezone=Europe/Paris --cleanup-database \
	--sales-order-increment-prefix="ORD$" --session-save=db --use-rewrites=1



