# Práctica RA 3.1 – Hardening de Apache en Docker

## Objetivo

El propósito de esta práctica es aplicar técnicas de **hardening en un servidor Apache**, reduciendo su superficie de ataque y mejorando su seguridad general. Para ello hemos realizado varias etapas:

1. Configuración de cabeceras de seguridad (CSP)
2. Instalación y configuración de un WAF (ModSecurity)
3. Protección básica frente a ataques DoS/DDoS
4. Instalación de certificado SSL
5. Aplicación de buenas prácticas de seguridad

Toda la práctica se ha realizado en contenedores Docker, construyendo varias imágenes que heredan unas de otras para crear un entorno seguro y reproducible.

## Enlaces de referencia

Guías utilizadas para documentar y validar las prácticas:

- [Hardening de servidor web Apache](https://psegarrac.github.io/Ciberseguridad-PePS/tema3/seguridad/web/2021/03/01/Hardening-Servidor.html)
  
- [Configuración de Certificado SSL en Apache](https://psegarrac.github.io/Ciberseguridad-PePS/tema1/practicas/2020/11/08/P1-SSL.html)

- [Buenas prácticas y hardening general en Apache](https://geekflare.com/cybersecurity/apache-web-server-hardening-security/)

## Enlace del repositorio de imágenes en Docker Hub

Puedes encontrar todas las imágenes generadas en:

- [Docker Hub](https://hub.docker.com/repository/docker/pps10830341/ra3.1/general)

(El enlace muestra todos los tags `pr1`, `pr2`, `pr3`, `pr4`, `pr5` y `pr6` que corresponden a las etapas de la práctica.)

- [Dockerfiel base (pr1)](https://hub.docker.com/repository/docker/pps10830341/ra3.1/tags/pr1/sha256:dd5a36c199b393852c50c156b98185c51d7492f0acba56ecf0469d26b6e6910f) (**sha256:** dd5a36c199b393852c50c156b98185c51d7492f0acba56ecf0469d26b6e6910f)

- [Dockerfiel final (pr6)](https://hub.docker.com/repository/docker/pps10830341/ra3.1/tags/pr6/sha256:eb553510c0386a5817f2583146d92998a983644192251a85e769fc067d83adfe) (**sha256:** eb553510c0386a5817f2583146d92998a983644192251a85e769fc067d83adfe)