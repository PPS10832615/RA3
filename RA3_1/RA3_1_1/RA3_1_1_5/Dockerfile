# Usamos una imagen de Nginx que ya incluya ModSecurity v3
FROM owasp/modsecurity-crs:nginx
USER root

# 1. Instalar PHP y utilidades
RUN apt-get update && \
    apt-get install -y php-fpm openssl apache2-utils && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 2. Cargar el módulo modsecurity
RUN sed -i '1i load_module modules/ngx_http_modsecurity_module.so;' /etc/nginx/nginx.conf

# 3. Fix para las reglas OWASP
RUN if [ -f /etc/modsecurity.d/owasp-crs/crs-setup.conf.example ]; then \
        mv /etc/modsecurity.d/owasp-crs/crs-setup.conf.example /etc/modsecurity.d/owasp-crs/crs-setup.conf; \
    fi

# 4. Directorios de logs php
RUN mkdir -p /run/php && \
    touch /var/log/php-fpm.log && \
    chown -R nginx:nginx /var/log/php-fpm.log /run/php

# 5. Configuración certificados SSL
RUN mkdir -p /etc/nginx/ssl && \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/nginx/ssl/nginx.key \
    -out /etc/nginx/ssl/nginx.crt \
    -subj "/C=ES/ST=Castellon/L=Castellon/O=IES/CN=localhost"

# 6. Auth
RUN htpasswd -bc /etc/nginx/.htpasswd admin Taller.2014

# 7. Copiar las configuraciones
# Copiamos la configuración de PHP pool
COPY config/www.conf /etc/php/8.2/fpm/pool.d/www.conf
# Copiamos configuraciones de Nginx
COPY config/default.conf /etc/nginx/conf.d/default.conf
COPY config/modsec_includes.conf /etc/nginx/modsec_includes.conf
COPY config/modsecurity.conf /etc/modsecurity.d/modsecurity.conf
# Copiamos la web
COPY pages/ /var/www/html/

# 8. Permisos
RUN chown -R nginx:nginx /var/www/html

EXPOSE 80 443

# 9. Arranque directo
CMD /usr/sbin/php-fpm8.2 -F & nginx -g "daemon off;"
