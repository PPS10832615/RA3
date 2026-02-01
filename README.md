# Seguridad en Servidores - RA3

Este repositorio contiene las prácticas y proyectos correspondientes al **Resultado de Aprendizaje 3 (RA3)**, enfocados en el despliegue de infraestructuras web seguras, bastionado de servidores y auditoría de perímetros.

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

Actualmente, el repositorio se centra en el bloque de Hardening de Servidores:

* **[RA3_1: Server Hardening Project](./RA3_1/README.md)**
  * Implementación de WAF (ModSecurity + OWASP CRS).
  * Mitigación de ataques DoS (mod_evasive).
  * Arquitecturas seguras con Apache y Nginx.
  * Gestión de identidades SSL/TLS.

---

## Requisitos del Entorno

Para replicar estos despliegues se requiere:
* **Docker** v27.5.1 o superior.
* **Docker Compose**.
* Acceso a terminal Linux.

---
