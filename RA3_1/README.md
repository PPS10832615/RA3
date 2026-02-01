![Version](https://img.shields.io/badge/version-v2026.01.02-6f42c1) ![Docker Version](https://img.shields.io/badge/docker-v27.5.1-2496ED?logo=docker&logoColor=white) ![Debian](https://img.shields.io/badge/debian-bookworm--slim-D70A53?logo=debian&logoColor=white) ![Apache](https://img.shields.io/badge/apache-2.4.62-bc4439?logo=apache&logoColor=white) ![Nginx](https://img.shields.io/badge/nginx-1.27-009639?logo=nginx&logoColor=white) ![PHP](https://img.shields.io/badge/php-8.2-8892bf?logo=php&logoColor=white)

# Server Hardening Project: RA3_1

Este repositorio documenta la evolución técnica de una infraestructura web, aplicando un endurecimiento progresivo desde una configuración base hasta un entorno blindado bajo el principio de **defensa en profundidad**.

---

## Hoja de ruta

A continuación se detalla la progresión de las actividades. Haga clic en el título de cada práctica para acceder a su documentación específica y archivos de configuración.

### Bloque RA3_1_1: Tecnologías base y WAF

* **[RA3_1_1_1: Cimientos y hardening base](./RA3_1_1/RA3_1_1_1/README.md)**
Optimización de cabeceras de respuesta y cifrado inicial.


* **[RA3_1_1_2: Web Application Firewall (WAF)](./RA3_1_1/RA3_1_1_2/README.md)**
Introducción de ModSecurity para el filtrado de tráfico en tiempo real.


* **[RA3_1_1_3: Inteligencia con OWASP CRS](./RA3_1_1/RA3_1_1_3/README.md)**
Integración de reglas avanzadas para mitigar SQLi, XSS y LFI.


* **[RA3_1_1_4: Resiliencia y Anti-DoS](./RA3_1_1/RA3_1_1_4/README.md)**
Mitigación de ataques de denegación de servicio mediante umbrales de tráfico.


* **[RA3_1_1_5: Modernización con Stack Nginx](./RA3_1_1/RA3_1_1_5/README.md)**
Migración a arquitectura Nginx optimizada con sockets TCP.



### Bloque RA3_1_2 e RA3_1_3: Identidad y blindaje

* **[RA3_1_2: Identidad SSL y gobernanza de red](./RA3_1_2/README.md)** * 
Gestión de certificados con identidad local y redirección permanente 301.


* **[RA3_1_3: Blindaje Final de Sistema](./RA3_1_3/README.md)**
Protocolos TLS 1.2+, ofuscación de banners y ejecución con usuario `apache`.



---

## Organización de Directorios

La estructura sigue la jerarquía normativa de la asignatura, facilitando la localización de cada `Dockerfile` y sus archivos de configuración:

```yaml
RA3/
└── RA3_1/
    ├── RA3_1_1/                    # Bloque I: Tecnologías Base y WAF
    │   ├── RA3_1_1_1/              # P1: Hardening inicial y SSL/TLS
    │   ├── RA3_1_1_2/              # P2: ModSecurity (Motor preventivo)
    │   ├── RA3_1_1_3/              # P3: Integración OWASP Core Rule Set
    │   ├── RA3_1_1_4/              # P4: Resiliencia con Anti-DoS (mod_evasive)
    │   ├── RA3_1_1_5/              # P5: Migración a Nginx + PHP-FPM
    │   └── README.md               
    ├── RA3_1_2/                    # Bloque II: Identidad y Cifrado (SSL & 301)
    ├── RA3_1_3/                    # Bloque III: Full Hardening (Blindaje final)
    └── README.md                   # Este archivo
```

---

## Catálogo de Despliegue (Docker Hub)

| Recurso | Puerto de Acceso | Imagen Oficial | Tecnología Clave |
| --- | --- | --- | --- |
| **P1** | `https://localhost:9001` | `pps:pr3111` | SSL/TLS Headers |
| **P2** | `https://localhost:9002` | `pps:pr3112` | ModSecurity v2 |
| **P3** | `https://localhost:9003` | `pps:pr3113` | OWASP CRS |
| **P4** | `https://localhost:9004` | `pps:pr3114` | mod_evasive |
| **P5** | `https://localhost:9005` | `pps:pr3115` | Nginx & PHP 8.2 |
| **P6** | `https://www.midominioseguro.com:9006` | `pps:pr312` | Redirección 301 |
| **P7** | `https://www.midominioseguro.com:9007` | `pps:pr313` | User Isolation |

---

## Validación del Entorno

Para que las pruebas de dominio funcionen correctamente en las últimas fases, edite su archivo de configuración local:

> **Archivo:** `/etc/hosts`
> `127.0.0.1   www.midominioseguro.com`
