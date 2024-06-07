# Nagios en Docker

Este Dockerfile crea una imagen para ejecutar Nagios, un sistema de monitoreo de red y sistemas, en un contenedor Docker. Incluye la configuración de Apache, Nagios Core, plugins de Nagios y otros componentes necesarios.

## Requisitos Previos

Antes de comenzar, asegúrate de tener Docker instalado en tu sistema. Si no lo tienes, puedes instalarlo siguiendo estas instrucciones:

### Instalación de Docker en Ubuntu

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo systemctl enable docker
```

## Construcción de la Imagen

Para construir la imagen Docker, navega hasta el directorio donde se encuentra el Dockerfile y ejecuta el siguiente comando:

```bash
docker build -t nagios:latest .
```

## Ejecución del Contenedor

Una vez que la imagen se ha construido, puedes ejecutar el contenedor con el siguiente comando:

```bash
docker run -d -p 80:80 -p 5667:5667 --name nagios \
-v /path/to/nagios/var:/opt/nagios/var \
-v /path/to/nagios/etc:/opt/nagios/etc \
-v /path/to/apache/log:/var/log/apache2 \
-v /path/to/custom/plugins:/opt/Custom-Nagios-Plugins \
-v /path/to/nagiosgraph/var:/opt/nagiosgraph/var \
-v /path/to/nagiosgraph/etc:/opt/nagiosgraph/etc \
nagios:latest
```

## Variables de Entorno

El Dockerfile utiliza varias variables de entorno para configurar Nagios y sus componentes. Aquí hay una lista de ellas y su propósito:

- `NAGIOS_HOME`: Directorio principal de Nagios.
- `NAGIOS_USER` y `NAGIOS_GROUP`: Usuario y grupo de Nagios.
- `NAGIOS_CMDUSER` y `NAGIOS_CMDGROUP`: Usuario y grupo para comandos de Nagios.
- `NAGIOS_FQDN`: Nombre de dominio completo para el servidor Nagios.
- `NAGIOSADMIN_USER` y `NAGIOSADMIN_PASS`: Credenciales para el usuario administrador de Nagios.
- `APACHE_RUN_USER` y `APACHE_RUN_GROUP`: Usuario y grupo para ejecutar Apache.
- `NAGIOS_TIMEZONE`: Zona horaria para Nagios.
- `DEBIAN_FRONTEND`: Configuración de frontend de Debian para evitar prompts durante la instalación.
- `NG_NAGIOS_CONFIG_FILE`, `NG_CGI_DIR`, `NG_WWW_DIR`, `NG_CGI_URL`: Directorios y URL de configuración de Nagios.
- `NAGIOS_BRANCH`, `NAGIOS_PLUGINS_BRANCH`, `NRPE_BRANCH`, `NCPA_BRANCH`, `NSCA_BRANCH`: Ramas específicas para las diferentes herramientas y plugins de Nagios.
- `NAGIOSTV_VERSION`: Versión de NagiosTV.

## Puertos Expuestos

El contenedor expone los siguientes puertos:

- `80`: Puerto HTTP para la interfaz web de Nagios.
- `5667`: Puerto para el NRPE (Nagios Remote Plugin Executor).

## Volúmenes

El contenedor utiliza varios volúmenes para persistir datos y configuraciones:

- `${NAGIOS_HOME}/var`: Datos de Nagios.
- `${NAGIOS_HOME}/etc`: Archivos de configuración de Nagios.
- `/var/log/apache2`: Logs de Apache.
- `/opt/Custom-Nagios-Plugins`: Plugins personalizados de Nagios.
- `/opt/nagiosgraph/var`: Datos de NagiosGraph.
- `/opt/nagiosgraph/etc`: Configuración de NagiosGraph.

## Comandos Adicionales

### Detener el Contenedor

```bash
docker stop nagios
```

### Eliminar el Contenedor

```bash
docker rm nagios
```

### Acceder al Contenedor

Para acceder al contenedor en ejecución:

```bash
docker exec -it nagios /bin/bash
```

## Contacto

Mantenedor: Javier Torres Oñate  
Email: [Javi.torres@duocuc.cl](mailto:Javi.torres@duocuc.cl)

---

Este archivo `readme.md` proporciona una guía completa para construir y ejecutar un contenedor Docker con Nagios, detallando todas las configuraciones y comandos necesarios para su correcta ejecución.
