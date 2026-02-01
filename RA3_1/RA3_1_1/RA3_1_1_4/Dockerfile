# 1. Usamos la imagen de la práctica anterior
FROM pps10832615/pps:pr3113

# 2. Instalación de herramientas
RUN apt-get update && \
    apt-get install -y libapache2-mod-evasive apache2-utils && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 3. Preparacion del directorio de logs
RUN mkdir -p /var/log/mod_evasive && \
    chown -R www-data:www-data /var/log/mod_evasive

# 4. Aplicamos nuestra configuración
COPY config/evasive.conf /etc/apache2/mods-available/evasive.conf

# 5. Habilitar el módulo
RUN a2enmod evasive

# CMD y EXPOSE se heredan (80, 443)
