# Seguridad en Servidores - RA3

Este repositorio contiene las prácticas y proyectos correspondientes al **Resultado de Aprendizaje 3 (RA3)**, enfocados en el despliegue de infraestructuras web seguras, bastionado de servidores y auditoría de vulnerabilidades web.

---

## Información del Autor

* **Nombre:** Roberto Pecurto Escrig
* **Usuario GitHub:** [PPS10832615](https://github.com/PPS10832615)
* **Asignatura:** Puesta en Producción Segura

---

## Repositorio de Imágenes (Docker Hub)

Todas las imágenes generadas durante este módulo están centralizadas en el siguiente repositorio oficial:

**[Docker Hub: pps](https://hub.docker.com/repository/docker/pps10832615/pps/general)**

*Nota: Las imágenes están etiquetadas siguiendo el esquema `pps:pr31xx` para cada fase del proyecto.*

---

## Contenido del Repositorio

El repositorio se divide en dos grandes bloques prácticos: Bastionado (Defensa) y Auditoría (Ataque):

* **[RA3_1: Server Hardening Project](./RA3_1/README.md)**
  * Implementación de WAF (ModSecurity + OWASP CRS).
  * Mitigación de ataques DoS (mod_evasive).
  * Arquitecturas seguras con Apache y Nginx.
  * Gestión de identidades SSL/TLS.

* **[RA3_2: Auditoría y Explotación Web con DVWA](./RA3_2/README.md)**
  * Análisis y explotación de vulnerabilidades web (basado en OWASP Top 10).
  * Técnicas de evasión de filtros (Bypass) en distintos niveles de seguridad.
  * Automatización de exfiltración de datos (Blind SQLi con Python).
  * Pruebas de concepto prácticas para XSS, CSRF, LFI, Command Injection, entre otros.

---

## Requisitos del Entorno

Para replicar estos despliegues y auditar las vulnerabilidades se requiere:
* **Docker** v27.5.1 o superior y **Docker Compose**.
* Acceso a terminal Linux (preferiblemente Kali Linux o similar).
* **Burp Suite** (Para la interceptación y manipulación de peticiones HTTP en RA3_2).
* **Python 3** (Para la ejecución de scripts de automatización).

---