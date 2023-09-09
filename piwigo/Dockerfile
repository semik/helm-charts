FROM httpd:2.4.57
RUN apt update && apt install -y procps wget unzip

# remove for production
RUN apt install -y bash

# add proper Debian sources
COPY bookworm.sources.list /etc/apt/sources.list

# add Ondrej Sury php repository
RUN wget https://packages.sury.org/php/apt.gpg -O /usr/share/keyrings/deb.sury.org-php.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/deb.sury.org-php.gpg] https://packages.sury.org/php/ bullseye main" > /etc/apt/sources.list.d/php.list

RUN apt update && apt install -y libapache2-mod-php7.4 php7.4-gd php7.4-mbstring php7.4-mysql php7.4-cli

# download piwigo
RUN wget "https://piwigo.org/download/dlcounter.php?code=13.8.0" -O /tmp/piwigo.zip
# extract piwigo
RUN cd /usr/local/apache2/htdocs/ && unzip /tmp/piwigo.zip && mv -f piwigo public-html

# apache config with fixed DocumentRoot to /var/www/html/piwigo
#tady to nikdo necte COPY 000-default.conf /etc/apache2/sites-available/

#CMD ["apache2-foreground"]