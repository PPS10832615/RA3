# 5. DOM Based Cross Site Scripting (XSS) - DVWA

El objetivo de esta práctica es explotar una vulnerabilidad de Cross-Site Scripting basada en el DOM (Document Object Model). A diferencia del XSS reflejado o almacenado, en el DOM XSS el payload malicioso no es necesariamente procesado por el servidor web, sino que es ejecutado directamente por el código JavaScript del lado del cliente en el navegador de la víctima.

## 1. Nivel LOW

### Análisis y explotación

En el nivel bajo, la página permite seleccionar un idioma mediante un menú desplegable. Al hacerlo, la selección se refleja en la URL a través del parámetro GET `default` (ej. `default=English`). 

Al no existir ninguna validación o sanitización del lado del cliente antes de procesar este parámetro en el DOM, podemos inyectar etiquetas HTML y JavaScript directamente en la URL.

* **Payload utilizado:** `default=<script>alert(document.cookie);</script>`

![Ejecución de DOM XSS en nivel Low](assets/0.1.png)
*Captura 1: Explotación exitosa en nivel bajo. El navegador procesa la etiqueta script y lanza una alerta mostrando la cookie de sesión de la víctima.*

---

## 2. Nivel MEDIUM

### Análisis de la vulnerabilidad

En este nivel, el servidor implementa un filtro básico que bloquea el uso de la etiqueta `<script>`. Además, el punto de inyección de nuestro parámetro se encuentra dentro de una etiqueta `<option>` perteneciente a un menú `<select>`.

### Evasión (Bypass)

Para que el ataque funcione, primero debemos "escapar" de la estructura HTML en la que estamos confinados cerrando las etiquetas correspondientes. Una vez fuera, como no podemos usar `<script>`, utilizamos un vector alternativo: inyectar una imagen rota (`<img>`) que ejecute código a través de un error (`onerror`). 

* **Payload utilizado:** `default=></option></select><img src=x onerror="alert(document.cookie)">`

![Evasión de filtros en nivel Medium usando una etiqueta img](assets/1.1.png)
*Captura 2: Bypass de las restricciones en nivel medio. Se escapan las etiquetas del selector y se fuerza la ejecución del JavaScript mediante el fallo de carga de una imagen ficticia.*

---

## 3. Nivel HIGH

### Análisis de la vulnerabilidad

En el nivel de seguridad alto, el servidor implementa una "lista blanca" (whitelist). Solo acepta valores estrictamente definidos (como "English", "French", etc.). Si enviamos etiquetas HTML al servidor, la petición será rechazada.

### Evasión mediante el "Fragmento"

La debilidad de este nivel reside en el desconocimiento de cómo funcionan las URLs en el navegador. Todo lo que se coloca después de una almohadilla `#` **no se envía al servidor web**, pero sí es procesado por el DOM en el cliente. 

Colocando nuestro payload detrás del `#`, evadimos completamente la whitelist del servidor, ya que este solo verá la petición principal, mientras que el navegador ejecutará el JavaScript localmente.

* **Payload utilizado:** `default=English#<script>alert(document.cookie);</script>`

![Evasión de lista blanca en nivel High usando el fragmento hash](assets/2.1.png)
*Captura 3: Explotación en nivel alto. El payload se oculta tras el símbolo "#", siendo invisible para los filtros del servidor web pero ejecutable por el motor DOM del navegador.*