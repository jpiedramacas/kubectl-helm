Para crear un README profesional que cumpla con tus requerimientos, aquí tienes el contenido detallado paso a paso:

---

# Despliegue de Aplicación con Helm en Kubernetes

Este README proporciona una guía paso a paso para desplegar una aplicación usando Helm en un clúster de Kubernetes. Se incluyen explicaciones detalladas de cada archivo de configuración, comandos para desplegar la aplicación, verificar su funcionamiento y realizar actualizaciones.

## Estructura del Proyecto

El proyecto está estructurado de la siguiente manera:

```
.
|-- Chart.yaml
|-- README.md
|-- templates
|   |-- NOTES.txt
|   |-- _helpers.tpl
|   |-- deployment.yaml
|   |-- service.yaml
|   `-- serviceaccount.yaml
`-- values.yaml
```

### Archivos de Configuración

1. **Chart.yaml**: Define los metadatos del chart, como el nombre, la versión y la descripción del chart.
   
2. **README.md**: Este archivo README que proporciona la documentación y guía de uso del chart.

3. **templates/**: Directorio que contiene los archivos YAML que definen los recursos de Kubernetes.

   - **NOTES.txt**: Instrucciones para los usuarios después de instalar el chart.
   - **_helpers.tpl**: Plantillas de ayuda utilizadas en otros archivos de configuración.
   - **deployment.yaml**: Archivo que define el Deployment de la aplicación, incluyendo la configuración del contenedor y las sondas de salud.
   - **service.yaml**: Archivo que define el Service para exponer la aplicación dentro del clúster.
   - **serviceaccount.yaml**: Archivo opcional que define la cuenta de servicio utilizada por la aplicación.

4. **values.yaml**: Archivo de valores por defecto para el chart, que permite personalizar la configuración de la aplicación, como el número de réplicas, la imagen del contenedor, y la política de extracción de la imagen.

## Despliegue de la Aplicación

Para desplegar la aplicación en Kubernetes usando Helm, sigue estos pasos:

### 1. Instalación del Chart

Ejecuta el siguiente comando para instalar el chart en Kubernetes:

```sh
helm install <nombre_release> . -f values.yaml
```

- `<nombre_release>` es el nombre que le darás a tu release en Kubernetes.

Este comando despliega la aplicación utilizando las configuraciones definidas en los archivos del chart y los valores especificados en `values.yaml`.

### 2. Verificación del Despliegue

Para verificar que la aplicación se ha desplegado correctamente, puedes utilizar los siguientes comandos de Kubernetes:

```sh
kubectl get pods
kubectl get services
```

Estos comandos te mostrarán los pods y servicios creados para la aplicación, respectivamente.

### 3. Acceso a la Aplicación

#### Usando `minikube service`

Si estás usando `minikube`, puedes utilizar el siguiente comando para abrir el servicio en tu navegador predeterminado:

```sh
minikube service <nombre_servicio>
```

- `<nombre_servicio>` es el nombre del servicio definido en `service.yaml`.

#### Usando `kubectl port-forward`

Alternativamente, puedes usar `kubectl port-forward` para acceder directamente a un pod:

```sh
kubectl port-forward pod/<nombre_pod> <puerto_local>:<puerto_pod>
```

- `<nombre_pod>` es el nombre del pod que deseas acceder.
- `<puerto_local>` es el puerto en tu máquina local.
- `<puerto_pod>` es el puerto en el pod donde está corriendo la aplicación.

### 4. Actualización de la Aplicación

Si necesitas actualizar la configuración de la aplicación, como cambiar la imagen del contenedor o ajustar los recursos, puedes utilizar el siguiente comando de Helm:

```sh
helm upgrade <nombre_release> . -f values.yaml
```

Este comando actualizará el release existente con las nuevas configuraciones definidas en `values.yaml`, sin necesidad de eliminar y volver a crear los recursos.

---

Este README proporciona una guía completa para desplegar, verificar y actualizar una aplicación en Kubernetes usando Helm. Asegúrate de ajustar los nombres y configuraciones específicas según tu caso de uso antes de ejecutar los comandos.
