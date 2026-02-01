# RA 3.1.1 – Medidas de Seguridad en Apache

## Objetivo

El objetivo del apartado **RA 3.1.1** es reforzar la seguridad del servidor web Apache mediante la aplicación de diferentes mecanismos de protección a nivel de aplicación.  
Estas medidas están orientadas a prevenir ataques comunes como:

- Inyecciones de código (SQL Injection)
- Manipulación de cabeceras HTTP
- Ataques de denegación de servicio (DoS/DDoS)
- Accesos no autorizados o comportamientos anómalos

Para ello se han implementado tres bloques principales:

1. Cabeceras de seguridad (CSP)  
2. Firewall de aplicaciones web (WAF)  
3. Protección frente a ataques DoS/DDoS  

## 1. Cabeceras de Seguridad – Content Security Policy (CSP)

Las **cabeceras de seguridad HTTP** permiten al servidor indicar al navegador cómo debe tratar el contenido recibido.  
Esto ayuda a prevenir ataques como la carga de recursos maliciosos externos.

Para centralizar estas cabeceras se ha creado un archivo de configuración específico en Apache:

````
/etc/apache2/conf-available/security-headers.conf
````

En este archivo se definen las siguientes cabeceras:

- **Content-Security-Policy**: Solo permite cargar recursos desde el propio servidor.
- **X-Content-Type-Options**: Evita que el navegador intente interpretar archivos como otro tipo distinto.
- **X-Frame-Options**: Impide que la web se cargue dentro de un iframe (protección contra clickjacking).
- **X-XSS-Protection**: Activa el filtro básico contra ataques XSS en el navegador.
- **Referrer-Policy**: Evita que se envíe información de la URL al navegar a otros sitios.

Una vez configurado el archivo, se habilita con el comando `a2enconf security-headers`.

Tras comprobar que la configuración no contiene errores, se recarga Apache.
La validación se realiza utilizando curl -I, comprobando que las cabeceras aparecen correctamente en la respuesta HTTP del servidor.

## 2. WAF – Web Application Firewall

Para añadir una capa adicional de protección se ha instalado ModSecurity, un firewall de aplicaciones web (WAF) para Apache.

El WAF analiza las peticiones HTTP en busca de patrones maliciosos, como:
- Inyecciones SQL.
- Intentos de ejecución de código.
- Peticiones sospechosas o mal formadas.

Se a instalación del módulo `libapache2-mod-security2`.

Se a copado el archivo de configuración recomendado.

Se a activado el motor de reglas en modo bloqueo (*SecRuleEngine On*).

Y se a habilitado el módulo en Apache.

Una vez activo, el WAF bloquea automáticamente las peticiones consideradas peligrosas.
Esto se comprueba realizando una solicitud con parámetros típicos de ataque, donde el servidor responde con un **403 Forbidden** o rechaza directamente la URL.

## 3. Protección frente a ataques DoS/DDoS (mod_evasive)

Para mitigar ataques de denegación de servicio, se ha instalado el módulo mod_evasive.

Este módulo detecta comportamientos anómalos como:
- Muchas peticiones repetidas desde una misma dirección IP.
- Accesos masivos en un intervalo de tiempo muy corto.

Cuando se superan los límites configurados, el módulo:
- Bloquea temporalmente la IP atacante.
- Reduce la carga del servidor.
- Protege la disponibilidad del servicio web.

La configuración se realiza en el archivo `/etc/apache2/mods-available/evasive.conf`.

En él se definen parámetros como:
- Número máximo de peticiones permitidas.
- Tiempo de espera entre peticiones.
- Tiempo durante el cual una IP estará bloqueada.

Estos valores permiten adaptar la protección sin afectar al uso normal de usuarios legítimos.