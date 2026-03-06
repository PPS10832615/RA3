# 12. Stored Cross Site Scripting (XSS) - DVWA

El objetivo de esta práctica es explotar una vulnerabilidad de Cross-Site Scripting Almacenado (Stored XSS). A diferencia del XSS Reflejado, aquí el código malicioso inyectado se guarda de forma permanente en la base de datos de la aplicación web. Cuando un usuario legítimo entra a leer los mensajes, su navegador descarga y ejecuta automáticamente el payload.

## 1. Nivel LOW

### Análisis y explotación

En el nivel de seguridad bajo, la aplicación web no realiza ninguna sanitización en los campos del formulario. Podemos inyectar código HTML y JavaScript directamente en el campo de texto ancho (`Message`).

Para evitar usar la clásica etiqueta `<script>`, empleamos una imagen rota que fuerza la ejecución de código a través de su manejador de errores. 

* **Payload utilizado:** `<img src=x onerror="alert(document.cookie)">`

![Inyección del payload en el nivel Low](assets/0.1.png)
*Captura 1: Inyección directa del payload en el campo Message del formulario, sin restricciones aparentes.*

Al firmar el libro de visitas (*Sign Guestbook*), el mensaje se guarda en la base de datos y se carga en la pantalla. Inmediatamente, el navegador intenta procesar la imagen rota y ejecuta el JavaScript, revelando la cookie de sesión del usuario.

![Ejecución del payload y robo de cookie](assets/0.2.png)
*Captura 2: Ejecución exitosa del XSS Almacenado. La alerta emerge automáticamente mostrando el valor de la cookie "security=low" tras publicarse el mensaje.*

---

## 2. Nivel MEDIUM

### Análisis de la vulnerabilidad y evasión (Bypass)

En el nivel medio, el desarrollador ha implementado medidas de seguridad en el campo `Message`, bloqueando ciertos caracteres. Sin embargo, el campo `Name` es vulnerable, pero cuenta con dos restricciones:
1. **Restricción de longitud en el cliente:** El campo HTML `<input>` tiene el atributo `maxlength="10"`, lo que impide pegar un payload completo.
2. **Filtro básico en el servidor:** El backend busca y elimina la etiqueta `<script>` exacta.

### Metodología de explotación

Primero, debemos evadir la restricción de longitud del lado del cliente. Para ello, utilizamos las Herramientas de Desarrollador del navegador (Inspect Element) para localizar el atributo `maxlength` del campo `Name` y modificar su valor o eliminarlo temporalmente.

![Modificación del DOM para evadir el maxlength](assets/1.1.png)
*Captura 3: Uso de las herramientas de desarrollador para alterar el código HTML del cliente, eliminando la restricción de longitud del atributo "maxlength" en el campo Name.*

Con la capacidad de escribir texto sin límite en el campo de nombre, evadimos el filtro del backend alterando las mayúsculas y minúsculas de nuestra etiqueta. Dado que el filtro busca estrictamente `<script>` en minúsculas, un payload mixto no será detectado, pero el navegador web lo interpretará igualmente.

* **Payload utilizado:** `<sCrIpT>alert(document.cookie);</ScRiPt>`

![Inyección del payload evadiendo filtros en el nivel Medium](assets/1.2.png)
*Captura 4: Inyección del payload ofuscado en el campo Name, aprovechando la modificación previa del DOM.*

Al enviar el formulario, el servidor acepta el texto y lo almacena. El navegador vuelve a cargar el libro de visitas y ejecuta nuestra etiqueta de script modificada, confirmando que la evasión ha funcionado.

![Ejecución del XSS en nivel Medium](assets/1.3.png)
*Captura 5: El ataque se completa con éxito, evadiendo el filtro de etiquetas y demostrando la ejecución del JavaScript reflejado en la cookie "security=medium".*