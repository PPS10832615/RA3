# 1. Imagen base de la practica anterior
FROM pps10832615/pps:pr3112

# 2. Instalación de las herramientas (git)
RUN apt-get update && \
    apt-get install -y git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 3. Descargar las reglas OWASP
RUN git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git /tmp/owasp-modsecurity-crs

# 4. Mover archivo de setup
RUN mv /tmp/owasp-modsecurity-crs/crs-setup.conf.example /etc/modsecurity/crs-setup.conf

# 5. Mover las reglas
RUN mkdir -p /etc/modsecurity/rules && \
    cp -r /tmp/owasp-modsecurity-crs/rules/* /etc/modsecurity/rules/

# 6. Aplicar nuestra configuración
COPY config/security2.conf /etc/apache2/mods-available/security2.conf

# 7. Activar unique_id
RUN a2enmod unique_id

# 8. Limpieza para que pese menos la imagen
RUN rm -rf /tmp/owasp-modsecurity-crs && \
    apt-get purge -y git && \
    apt-get autoremove -y

# CMD y Expose se heredan
