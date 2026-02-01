# Proyecto de Seguridad en Servidores Web (RA 3.1.1.1 - RA 3.1.1.5)

Esta sección contiene la evolución técnica de un servidor web seguro, aplicando capas de defensa en profundidad. El proyecto se divide en cinco fases incrementales, comenzando por el hardening básico de Apache y culminando en un entorno de alto rendimiento con Nginx y ModSecurity v3.

## Índice de Prácticas

| Identificador | Título Técnico | Tecnologías Clave |
| --- | --- | --- |
| **[RA 3.1.1.1](./RA3_1_1_1/README.md)** | Hardening Base de Apache | Apache, Headers, SSL |
| **[RA 3.1.1.2](./RA3_1_1_2/README.md)** | WAF Avanzado con ModSecurity | ModSecurity, OWASP CRS |
| **[RA 3.1.1.3](./RA3_1_1_3/README.md)** | WAF Avanzado con OWASP CRS | Core Rule Set, Git Automation |
| **[RA 3.1.1.4](./RA3_1_1_4/README.md)** | Mitigación de Ataques DoS | mod_evasive, Apache Bench |
| **[RA 3.1.1.5](./RA3_1_1_5/README.md)** | Stack Nginx + PHP-FPM Seguro | Nginx, ModSecurity v3, PHP 8.2 |

---

## 🛠️ Conceptos de Seguridad Implementados

### 1. Defensa Perimetral y WAF

A lo largo de las prácticas se ha integrado **ModSecurity** para actuar como firewall de aplicación. Se ha pasado de reglas manuales a la integración del **OWASP Core Rule Set (CRS)**, permitiendo la detección y bloqueo de:

* Inyecciones SQL (SQLi).
* Cross-Site Scripting (XSS).
* Inyección de Comandos y Path Traversal.

### 2. Cifrado y Confidencialidad (SSL/TLS)

Todas las prácticas implementan el protocolo HTTPS mediante la generación de certificados **SSL/TLS**. Se ha configurado el endurecimiento de protocolos (TLS 1.2+) y cifrados fuertes para evitar ataques de tipo *Man-in-the-Middle*.

### 3. Endurecimiento de Cabeceras (Hardening)

Se han inyectado cabeceras de seguridad en las respuestas HTTP para proteger al cliente final:

* **HSTS:** Fuerza el uso de HTTPS permanentemente.
* **CSP:** Define fuentes de contenido confiables para prevenir XSS.
* **X-Frame-Options:** Previene ataques de Clickjacking.

### 4. Disponibilidad y Control de Tráfico

Mediante el uso de **mod_evasive**, se han establecido umbrales de tráfico para identificar y bloquear automáticamente direcciones IP que realicen ataques de denegación de servicio (DoS) o fuerza bruta.

---

## 📝 Requisitos del Entorno

* **Docker / Docker Compose** instalado.
* **Resolución de nombres:** Se recomienda mapear `127.0.0.1` a los dominios de prueba en el archivo `/etc/hosts` para validar correctamente los certificados SSL.
