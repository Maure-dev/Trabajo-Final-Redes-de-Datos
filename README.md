# Trabajo-Final-Redes-de-Datos

### Trabajo Integrador Final - Redes de Datos

# Índice

1. [Integrantes del Proyecto](#integrantes-del-proyecto)
2. [Descripción del Proyecto](#descripción-del-proyecto)
3. [Objetivo](#objetivo)
4. [Estructura del Proyecto](#estructura-del-proyecto)
5. [Instalación y Configuración](#instalación-y-configuración)
6. [Uso del Proyecto](#uso-del-proyecto)
7. [Licencia](#licencia)

## Integrantes del Proyecto

- **Mauro Alejandro Gerardi**

- **Javier Ignacio Gerol**

- **Brian Leonel Retamar**

## Descripción del Proyecto

Este proyecto es una aplicación realizada con NGINX y Docker.

## Objetivo

Esta es la página que se utilizará para realizar las pruebas de rendimiento entre HTTP/1.1 y HTTP/2.

Esta página permite realizar las pruebas de carga y medir el impacto en tiempos de respuesta y cantidad de solicitudes bajo los dos protocolos.

## Estructura del Proyecto

La estructura del proyecto es la siguiente:

- `nginx-http1.1`: Contiene los archivos utilizados para iniciar un proyecto NGINX en HTTP/1.1.

- `nginx-http2`: Contiene los archivos utilizados para iniciar un proyecto NGINX en HTTP/2.

## Instalación y Configuración

Para instalar y configurar el proyecto, sigue estos pasos:

### 1. **Instalar Docker**

Si aún no tienes Docker instalado, sigue estos pasos para instalarlo:

- [Docker Desktop](https://www.docker.com/products/docker-desktop/)

### 2. **Verificar la instalación**

Para asegurarte de que Docker se instaló correctamente, verifica la versión con:

```bash
docker --version
```

Esto debería mostrar algo como Docker version 20.xx.

### 3. **Generar certificados autofirmados**

Puedes usar OpenSSL para generar un certificado autofirmado y una clave privada. Ejecuta estos comandos desde la raíz del proyecto:

```bash
cd nginx-http1.1
mkdir ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ssl/nginx-selfsigned.key -out ssl/nginx-selfsigned.crt -subj "/CN=localhost"
```

```bash
cd nginx-http2
mkdir ssl
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ssl/nginx-selfsigned.key -out ssl/nginx-selfsigned.crt -subj "/CN=localhost"
```

### 4. **Construir la imagen de Docker**

En la terminal, dentro del directorio donde están tus archivos Dockerfile y default.conf, del protocolo a levantar ejecuta el siguiente comando para construir la imagen de Nginx con soporte para HTTP/1.1 o HTTP/2:

- HTTP/1.1

  ```bash
  docker build -t nginx-http1.1 .
  ```

- HTTP/2

  ```bash
  docker build -t nginx-http2 .
  ```

### 5. **Correr el contenedor de Nginx**

Una vez que la imagen esté construida, ejecuta el siguiente comando para iniciar el contenedor:

- HTTP/1.1

  ```bash
  docker run --name nginx-http1.1 -p 6060:6060 -p 444:444 -d nginx-http1.1
  ```

  Esto expondrá los puertos 6060 (HTTP) y 444 (HTTPS) en tu máquina local.

- HTTP/2

  ```bash
  docker run --name nginx-http2 -p 8080:8080 -p 443:443 -d nginx-http2
  ```

  Esto expondrá los puertos 8080 (HTTP) y 443 (HTTPS) en tu máquina local.

## Uso del Proyecto

Una vez iniciado el proyecto, puedes acceder a la página principal en:

- HTTP/1.1

  https://localhost:444/

- HTTP/2

  https://localhost:445/

\*_Si tu navegador te advierte que el certificado no es de confianza, podés avanzar de forma segura, ya que es un certificado autofirmado._

### 6. **Verificar que protocolo está habilitado**

Abre tu navegador y accede a la URL mencionada en el paso 5. Si todo está configurado correctamente, podrás ver el contenido por HTTPS. Usa el inspector de red del navegador (F12, pestaña “Red” o "Network") para verificar que el protocolo que se está usando es "http/1.1" (HTTP/1.1) o "h2" (HTTP/2).

En caso de no visualizar la columna "Protocolo" o "Protocol" dar clic derecho en la tabla y habilitar la columna mencionada.

## Licencia

Este proyecto está bajo la Licencia MIT. Véase el archivo LICENSE.
