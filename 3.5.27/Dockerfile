FROM php:7-apache

LABEL version="0.1.1" \
	description="Docker Image for a contao installation version 3.5.27" \
	maintainer="Holger Janßen-Kroll <docker@ho-jk.de>"


# install the PHP extensions we need
RUN set -ex; \
	\
	apt-get update; \
	apt-get install -y \
		libicu-dev \
		libjpeg-dev \
		libpng12-dev \
		libgmp-dev \
		libmcrypt-dev \
		libxml2-dev \
		mysql-common \
		libbz2-dev \
		zlib1g-dev \
		vim \
	; \
	apt-get clean; \
	rm -rf /var/lib/apt/lists/*; \
	\
	ln -s /usr/include/x86_64-linux-gnu/gmp.h /usr/local/include/; \
	export CFLAGS="-I/usr/src/php" ;\
	docker-php-ext-configure gd --with-png-dir=/usr --with-jpeg-dir=/usr; \
	docker-php-ext-install pdo pdo_mysql gd mysqli gmp bcmath zip mcrypt xmlwriter xmlreader iconv bz2 mbstring soap intl 

RUN a2enmod rewrite expires


ENV VERSION 3.5.27

RUN set -ex; \
	curl -o contao.tar.gz -fSL "https://download.contao.org/${VERSION}/tar"

RUN set -ex; \
	tar -xzf contao.tar.gz -C /var/www/html; \
	rm contao.tar.gz; \
	chown -R www-data:www-data /var/www/html; \
	mv /var/www/html/contao-${VERSION}/* /var/www/html/; \
	mv /var/www/html/contao-${VERSION}/.e* /var/www/html/; \
	mv /var/www/html/contao-${VERSION}/.g* /var/www/html/; \
	mv /var/www/html/contao-${VERSION}/.h* /var/www/html/; \
	rmdir /var/www/html/contao-${VERSION}/; \

        # enable url rewriting
	cp -p /var/www/html/.htaccess.default .htaccess; \

	# write contao logs to std error
	ln -sfT /dev/stderr /var/www/html/system/logs/error.log
	#perl -pi -e "s#TL_ROOT\\s*.\\s*.'/system/logs/error.log'#'/dev/stderr'#" /var/www/html/system/initialize.php ; 

VOLUME /var/www/html


CMD ["apache2-foreground"]
