# RA 3.2 - Auditoría y Explotación Web con DVWA

Este repositorio contiene la documentación técnica y las evidencias prácticas de la explotación de múltiples vulnerabilidades web utilizando el entorno de pruebas **Damn Vulnerable Web Application (DVWA)**. 

El objetivo principal de este proyecto es comprender el funcionamiento interno de los fallos de seguridad más críticos en aplicaciones web (basados en el OWASP Top 10), analizando tanto su explotación básica como las técnicas necesarias para evadir filtros de seguridad incompletos o mal configurados.

---

## 📑 Índice de Vulnerabilidades

A continuación, se detalla el listado de vulnerabilidades explotadas. Haz clic en cada enlace para acceder a la memoria técnica, la metodología paso a paso y las evidencias gráficas de cada vector de ataque.

1. **[Brute Force](./1.BruteForce/README.md)** - Evasión de retardos intencionados del servidor para obtener credenciales válidas.
2. **[Command Injection](./2.CommandInjection/README.md)** - Ejecución remota de comandos en el sistema operativo subyacente mediante concatenación.
3. **[Content Security Policy (CSP) Bypass](./3.ContentSecurityPolicyBypass/README.md)** - Ejecución de código arbitrario evadiendo políticas de seguridad mediante nonces estáticos.
4. **[Cross Site Request Forgery (CSRF)](./4.CrossSiteRequestForgery/README.md)** - Secuestro de sesión forzando cambios de credenciales mediante validaciones de origen defectuosas.
5. **[DOM Based XSS](./5.DOMbasedCrossSiteScripting/README.md)** - Inyección de código JavaScript directamente en el entorno del navegador de la víctima.
6. **[File Inclusion](./6.FileInclusion/README.md)** - Lectura de archivos críticos del sistema mediante Local File Inclusion (LFI) y Path Traversal.
7. **[File Upload](./7.FileUpload/README.md)** - Subida de ejecutables maliciosos y obtención de Reverse Shell falsificando cabeceras MIME.
8. **[JavaScript Attacks](./8.JavaScriptAttacks/README.md)** - Manipulación de la lógica de validación criptográfica en el lado del cliente.
9. **[Reflected XSS](./9.ReflectedCrossSiteScriptingXSS/README.md)** - Ejecución de scripts evadiendo filtros de palabras clave en el servidor.
10. **[SQL Injection](./10.SQLinjection/README.md)** - Volcado de la base de datos inyectando sentencias lógicas en parámetros POST numéricos.
11. **[Blind SQL Injection](./11.SQLinjectionBlind/README.md)** - Exfiltración automatizada de datos a ciegas mediante scripts de Python.
12. **[Stored XSS](./12.StoredCrossSiteScriptingXSS/README.md)** - Inyección de código persistente en la base de datos evadiendo límites de longitud del DOM.
13. **[Weak Session IDs](./13.WeakSessionIDs/README.md)** - Predicción de tokens de sesión y análisis de generación basada en UNIX Timestamps.

---