
# Docker Compose para Desarrollo de WordPress con LEMP

Este README proporciona una guía detallada para configurar y utilizar un entorno de desarrollo local para WordPress usando Docker Compose. El proyecto incluye configuraciones para Nginx, PHP, MySQL y WordPress.

## Estructura del Proyecto

```
.
|-- README.md
|-- docker-compose.yml
|-- nginx/
|   |-- certs/
|   |   `-- README.md
|   `-- default.conf
|-- nginx.dockerfile
|-- php/
|   `-- www.conf
|-- php.dockerfile
`-- wordpress/
    `-- README.md
```

### Descripción de Archivos y Directorios

1. **README.md**: Este archivo que estás leyendo ahora, que proporciona documentación y guía de uso del proyecto.
   
2. **docker-compose.yml**: Archivo principal de Docker Compose que define los servicios y configuraciones para los contenedores de Nginx, PHP, MySQL y WordPress.

3. **nginx/**:
   - **default.conf**: Archivo de configuración de Nginx para la configuración por defecto del servidor web.
   - **certs/**: Directorio que puede contener certificados SSL/TLS (consultar README.md interno para más detalles).

4. **nginx.dockerfile**: Archivo Dockerfile para construir una imagen personalizada de Nginx (opcional).

5. **php/**:
   - **www. conf**: Archivo de configuración de PHP-FPM para la gestión de pools de PHP.

6. **php.dockerfile**: Archivo Dockerfile para construir una imagen personalizada de PHP (opcional).

7. **wordpress/**:
   - **README.md**: Documentación específica para WordPress que guía la instalación y configuración de la aplicación.

## Uso

Para comenzar, asegúrate de tener Docker instalado en tu sistema y luego sigue estos pasos detallados:

### 1. Configurar y Desplegar los Contenedores

Desde el directorio raíz del proyecto, ejecuta el siguiente comando para construir e iniciar los contenedores del servidor web:

```bash
eval $(minikube docker-env)
```

```bash
docker-compose up -d --build site
```

Este comando inicia los contenedores necesarios para Nginx, PHP, MySQL y WordPress. El servicio `site` se enfoca únicamente en los contenedores de tu sitio web.

### 2. Configuración de WordPress

Una vez que los contenedores estén en ejecución, sigue estos pasos para configurar tu instalación de WordPress:

- Accede a tu navegador web y visita `http://localhost`. Deberías ver la pantalla de configuración inicial de WordPress.
- Sigue las instrucciones en pantalla para configurar la conexión a la base de datos MySQL y para configurar el sitio de WordPress.

### 3. Acceso a los Servicios

Los servicios se exponen en los siguientes puertos:

- **Nginx**: `http://localhost`
- **MySQL**: Puerto estándar MySQL (por defecto: `3306`)
- **PHP-FPM**: Puerto estándar PHP-FPM (por defecto: `9000`)

Puedes acceder a tu sitio de WordPress a través de `http://localhost` en tu navegador web.


---

Este README proporciona una guía completa para configurar y utilizar un entorno de desarrollo local para WordPress usando Docker Compose. Asegúrate de personalizar los nombres de directorios y ajustar las configuraciones según tus necesidades específicas antes de ejecutar los comandos.
