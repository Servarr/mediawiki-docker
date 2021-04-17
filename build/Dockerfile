FROM mediawiki:1.35

RUN apt-get update && apt-get install -y --no-install-recommends \
        unzip \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apt/archives/* \s

RUN curl -Ls https://getcomposer.org/installer -o installer && \
        php installer --1 && \
        php composer.phar install --no-dev && \
        chmod a+x composer.phar && \
        mv composer.phar /usr/bin/composer && \
        rm installer

RUN git clone --depth 1 -b REL1_35 \
        https://gerrit.wikimedia.org/r/p/mediawiki/extensions/TemplateWizard \
        /var/www/html/extensions/TemplateWizard

RUN git clone --depth 1 -b REL1_35 \
        https://gerrit.wikimedia.org/r/mediawiki/extensions/LabeledSectionTransclusion.git \ 
        /var/www/html/extensions/LabeledSectionTransclusion

RUN git clone --depth 1 -b REL1_35 \
        https://gerrit.wikimedia.org/r/mediawiki/extensions/DismissableSiteNotice \
        /var/www/html/extensions/DismissableSiteNotice

RUN git clone --depth 1 -b REL1_35 \
        https://gerrit.wikimedia.org/r/mediawiki/extensions/PageNotice \
        /var/www/html/extensions/PageNotice

RUN git clone --depth 1 \
        https://github.com/Telshin/Spoilers.git \
        /var/www/html/extensions/Spoilers

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
        composer update jeroen/megdiawiki-github --no-dev -o && \
        chmod 777 /var/www/html/vendor/ezyang/htmlpurifier/library/HTMLPurifier/DefinitionCache/Serializer

RUN git clone --depth 1 -b master \
        https://github.com/Servarr/aether-mediawiki.git \
        /var/www/html/skins/aether && \
        cd /var/www/html/skins/aether && \
        composer install

COPY ./block-files.conf /etc/apache2/conf-enabled
