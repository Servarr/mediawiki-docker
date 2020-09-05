FROM mediawiki:latest

RUN apt-get update && apt-get install -y --no-install-recommends \
        unzip \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apt/archives/* \s

RUN curl -L https://getcomposer.org/installer | php \
        && php composer.phar install --no-dev && \
        chmod a+x composer.phar && \
        mv composer.phar /usr/bin/composer

RUN git clone --depth 1 \
        https://gerrit.wikimedia.org/r/p/mediawiki/extensions/TemplateData \
        /var/www/html/extensions/TemplateData

RUN git clone --depth 1 \
        https://gerrit.wikimedia.org/r/p/mediawiki/extensions/TemplateWizard \
        /var/www/html/extensions/TemplateWizard

RUN git clone --depth 1 \
        https://github.com/Schine/MW-OAuth2Client.git \
        /var/www/html/extensions/MW-OAuth2Client && \
        cd /var/www/html/extensions/MW-OAuth2Client && \
        git submodule update --init && \
        cd vendors/oauth2-client && \
        composer install

RUN git clone --depth 1 \
        https://github.com/ciencia/mediawiki-extensions-SaneCase.git \
        /var/www/html/extensions/SaneCase

RUN cd /var/www/html && \
        COMPOSER=composer.local.json composer require --no-update jeroen/mediawiki-github "~1.4" && \
        composer update jeroen/megdiawiki-github --no-dev -o

RUN git clone --depth 1 -b master \
        https://github.com/Servarr/aether-mediawiki.git \
        /var/www/html/skins/aether && \
        cd /var/www/html/skins/aether && \
        composer install
