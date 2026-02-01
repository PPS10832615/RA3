# Usamos la imagen anterior para poder heredar la seguridad ya configurada
FROM pps10832615/pps:pr3114

# Instalamos openssl
RUN apt-get update && \
    apt-get install -y openssl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Activar el módulo SSL
RUN a2enmod ssl

# Crear directorio para certificados
RUN mkdir -p /etc/apache2/ssl

# Generar la clave y certificado
# Inyectamos los datos de Castellón directamente
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/apache2/ssl/apache.key \
    -out /etc/apache2/ssl/apache.crt \
    -subj "/C=ES/ST=Castellon/L=Castellon de la Plana/O=IES El Caminas/OU=Departament of Server Development/CN=www.midominioseguro.com"

# Copiar la configuración mejorada (con redirección)
COPY config/default-ssl.conf /etc/apache2/sites-available/default-ssl.conf

# Activar el host virtual SSL y desactivar el default antiguo
RUN a2dissite 000-default.conf && a2ensite default-ssl.conf

# Puertos
EXPOSE 80 443

# El CMD se hereda, no hace falta ponerlo
