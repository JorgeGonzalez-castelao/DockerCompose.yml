# Guía de instalación de Odoo Service

Esta guía proporciona instrucciones para configurar y ejecutar un servicio Odoo utilizando Docker Compose. El servicio se ejecutará en un contenedor Odoo y utilizará un contenedor PostgreSQL como base de datos.

## Requisitos previos
- Docker
- Docker Compose

## Pasos de instalación

1. **Clonar el repositorio**: Clona el repositorio que contiene el archivo `docker-compose.yml` en tu máquina local.

```bash
git clone <URL_del_repositorio>
cd <nombre_del_directorio>
```

2. **Configurar el archivo docker-compose.yml**: Abre el archivo `docker-compose.yml` en un editor de texto y ajusta los nombres de los servicios y las variables de entorno según sea necesario. 

```yaml
version: '3.1'

services:
  # Cambiar 'webs2_dev' por el nombre deseado para el servicio Odoo
  nombre_del_servicio:
    image: odoo:16.0
    depends_on:
      - nombre_del_servicio_bd
    volumes:
      - ./extra-addons:/mnt/extra-addons
    ports:
      - "8069:8069"
    environment:
      - HOST=nombre_del_servicio_bd # mismo nombre que el servicio postgres
      - USER=odoo
      - PASSWORD=odoo

  # Cambiar 'mydbs2_dev' por el nombre deseado para el servicio PostgreSQL
  nombre_del_servicio_bd:
    image: postgres
    ports:
      - "5432:5432"
    environment:
      POSTGRES_DB: postgres
      POSTGRES_PASSWORD: odoo
      POSTGRES_USER: odoo
```

3. **Ejecutar el servicio**: Desde la terminal, dentro del directorio donde se encuentra el archivo `docker-compose.yml`, ejecuta el siguiente comando:

```bash
docker-compose up -d
```

Este comando descargará las imágenes necesarias, creará y ejecutará los contenedores según la configuración proporcionada en el archivo `docker-compose.yml`.

4. **Acceder a Odoo**: Una vez que los contenedores estén en funcionamiento, puedes acceder a Odoo en tu navegador web ingresando la siguiente dirección:

```
http://localhost:8069
```

## Notas adicionales

- El archivo `docker-compose.yml` proporcionado está configurado para ejecutar Odoo en el puerto `8069`. Si deseas cambiar el puerto de acceso, puedes modificar la sección `ports` dentro del servicio Odoo en el archivo `docker-compose.yml`.
- La carpeta `extra-addons` se monta en el contenedor de Odoo para agregar módulos adicionales. Puedes colocar tus propios módulos en esta carpeta para que se carguen en Odoo durante la ejecución.
- Asegúrate de tener los puertos `5432` y `8069` disponibles en tu máquina local, ya que estos son los puertos utilizados por PostgreSQL y Odoo respectivamente.

¡Ahora deberías tener un servicio Odoo en funcionamiento listo para ser utilizado! Si encuentras algún problema durante la instalación, asegúrate de revisar la configuración y los pasos proporcionados en esta guía.