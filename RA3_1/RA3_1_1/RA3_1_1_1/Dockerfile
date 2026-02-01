# Usamos Debian Bookworm una versión más ligera de Debian
FROM debian:bookworm-slim

# 1. Actualizar e instalar Apache y utilidades básicas
RUN apt-get update && \
    apt-get install -y apache2 curl openssl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 2. Preparar el directorio de certificados
RUN mkdir -p /etc/apache2/ssl

# 3. Copiar nuestros certificados
COPY ssl/mi_certificado.crt /etc/apache2/ssl/
COPY ssl/mi_clave.key /etc/apache2/ssl/

# 3. Copiar nuestras configuraciones
COPY config/hardening.conf /etc/apache2/conf-available/hardening.conf
COPY config/sitio-ssl.conf /etc/apache2/sites-available/sitio-ssl.conf

# 4. APLICAR HARDENING Y CONFIGURACIÓN
RUN a2enmod ssl headers
RUN a2enconf hardening
RUN a2disconf security
RUN a2ensite sitio-ssl
RUN a2dismod -f autoindex

# 5. Exponer puertos
EXPOSE 80 443

# 6. Arrancar Apache
CMD ["apache2ctl", "-D", "FOREGROUND"]
