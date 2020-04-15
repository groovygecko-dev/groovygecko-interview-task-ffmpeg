FROM php:7.4-fpm

ENV PHPREDIS_URL="https://github.com/phpredis/phpredis/archive/5.1.1.tar.gz"
ENV PHPREDIS_SHA256="6b054e1c944f0c415a3489cf6ac94d5423b2b506d8c36ac7a8cdd965a1c07cf9"

RUN apt-get update -y \
# Install dependencies
 && apt-get install -y \
        # FFMPEG
        ffmpeg \
        libavcodec-extra \
        # php-zip extension
        zlib1g-dev \
        libzip-dev \
        # php intl extension
        libicu-dev \

# Download, verify and copy phpredis
 && curl -fsSL -o phpredis.tar.gz "$PHPREDIS_URL" \
 && echo "$PHPREDIS_SHA256 *phpredis.tar.gz" | sha256sum -c - \
 && mkdir -p /usr/src/php/ext/redis \
 && tar -xzf phpredis.tar.gz -C /usr/src/php/ext/redis  --strip-components=1 \
 && rm phpredis.tar.gz \
 && echo 'redis' >> /usr/src/php-available-exts \
# Configure extensions
 && docker-php-ext-configure zip \
# Install extensions
 && docker-php-ext-install -j$(nproc) \
        redis \
        zip \
        intl

# Install Composer
ENV COMPOSER_URL="https://getcomposer.org/download/1.10.1/composer.phar"
ENV COMPOSER_SHA256="1831f266580f221189dc04d4b58d7fc50c934ffc3a0eca89ecb4a53aa44867e2"

RUN set -eux; \
    curl -fsSL -o composer.phar "$COMPOSER_URL"; \
    echo "$COMPOSER_SHA256 *composer.phar" | sha256sum -c -; \
    mv composer.phar /usr/bin/composer; \
    chmod +x /usr/bin/composer; \
    composer global require -q hirak/prestissimo
