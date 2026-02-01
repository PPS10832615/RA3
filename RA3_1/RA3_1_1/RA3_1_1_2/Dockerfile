# Se usa la imagen anterior para heredar las configuraciones
FROM pps10832615/pps:pr3111

# 1. Instalar ModSecurity (WAF)
RUN apt-get update && \
    apt-get install -y libapache2-mod-security2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 2. Configuración base
# Renombramos la configuración recomendada para que ModSecurity arranque con valores por defecto
RUN cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf

# 3. Inyectar configuración personalizada
# Copiamos el archivo de reglas en la carpeta config
COPY config/modsecurity_custom.conf /etc/apache2/conf-available/modsecurity_custom.conf

# 4. Habilitar módulo y configuración
RUN a2enmod security2 && \
    a2enconf modsecurity_custom

# CMD y EXPOSE se heredan de la imagen base (80, 443)
