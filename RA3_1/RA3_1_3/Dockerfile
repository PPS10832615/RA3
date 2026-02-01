# Usamos la imagen con todas las configuraciones acumuladas
FROM pps10832615/pps:pr312

# 1. Habilitar módulos necesarios
RUN a2enmod headers rewrite

# 2. Deshabilitar modulos innecesarios
RUN a2dismod dav dav_fs info autoindex -f || true

# 3. Creación de un usuario y un grupo llamado apache
RUN groupadd apache && \
    useradd -g apache -d /var/www/html -s /sbin/nologin apache

# 4. Configuración Apache para usar este usuario en vez de www-data
RUN sed -i 's/export APACHE_RUN_USER=www-data/export APACHE_RUN_USER=apache/g' /etc/apache2/envvars && \
    sed -i 's/export APACHE_RUN_GROUP=www-data/export APACHE_RUN_GROUP=apache/g' /etc/apache2/envvars

# 5. Permisos de directorios /conf y /bin
RUN chmod -R 750 /etc/apache2 && \
    chown -R apache:apache /var/log/apache2 /var/run/apache2 /var/lock/apache2 /var/www/html

# 6. Aplicar nuestra configuración
COPY config/hardening.conf /etc/apache2/conf-available/hardening.conf
RUN a2enconf hardening

# 7. Aplicar hardening ssl sobreescribiendo el anterior
COPY config/final-ssl.conf /etc/apache2/sites-available/default-ssl.conf

# 8. Limpieza de cabeceras
RUN echo "ServerTokens Prod" >> /etc/apache2/apache2.conf && \
    echo "ServerSignature Off" >> /etc/apache2/apache2.conf

EXPOSE 80 443
