FROM php:7.2-fpm-alpine

RUN apk update && apk add \
    git libmcrypt-dev \
    libvpx-dev libpng-dev \
    libxpm-dev \
    libxml2-dev \
    unixodbc-dev \
    libsodium-dev libxslt libxslt-dev

# Set timezone
#RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN "date"

# Type docker-php-ext-install to see available extensions
RUN docker-php-ext-install mbstring \
    pdo \
    pdo_mysql \
    bcmath \
    soap \
    xsl

RUN apk add --update curl-dev

RUN docker-php-ext-install curl \
    json \
    xml \
    zip

RUN apk add --update zip bzip2 libbz2 bzip2-dev

RUN docker-php-ext-install bz2 \
    exif \
    sodium

RUN apk add --update icu icu-dev

RUN docker-php-ext-install intl

RUN apk add --update freetype-dev \
                                 libjpeg-turbo-dev \
                                 libpng-dev

RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ --enable-exif
RUN docker-php-ext-install -j$(nproc) gd

RUN pear upgrade pear
RUN pear channel-discover pear.symfony-project.com
RUN pear install PHP_CodeSniffer

#RUN pecl install xdebug
#RUN docker-php-ext-enable xdebug

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer --version

# Install Node, Yarn
#RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
#RUN apt-get install -y nodejs
#RUN npm install -g yarn

WORKDIR /var/www/magento
