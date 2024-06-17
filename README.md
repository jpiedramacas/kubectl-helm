Aquí tienes una versión mejorada y más detallada del README para configurar Prometheus y Grafana en Minikube:

---

# Configuración de Prometheus y Grafana en Minikube

## Introducción

En esta guía, te mostraré cómo desplegar Prometheus y Grafana en tu clúster de Minikube utilizando sus gráficos Helm proporcionados. Prometheus nos ayudará a monitorear nuestro clúster de Kubernetes y otros recursos que se ejecutan en él. Grafana nos permitirá visualizar las métricas registradas por Prometheus y mostrarlas en paneles atractivos.

**Última actualización del artículo:** 2023-09-20, gracias a Dennis Eller por su contribución.

## Requisitos

- Minikube
- Helm

## Paso 1: Instalar Prometheus

Los gráficos de canal estable de Prometheus han sido desaprobados a favor de los Gráficos Helm de la Comunidad de Prometheus.

Comenzaremos añadiendo el repositorio a nuestra configuración de Helm:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

Una vez que el repositorio esté listo, podemos instalar los gráficos proporcionados ejecutando los siguientes comandos:

```bash
helm install prometheus prometheus-community/prometheus
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-np
```

El primer comando instala los gráficos. Tomará un tiempo hasta que todo esté desplegado. Podemos verificar el estado ejecutando:

```bash
kubectl get pods -l app.kubernetes.io/instance=prometheus
```

Dado que estamos utilizando Minikube, el segundo comando expone el servicio `prometheus-server` utilizando un `NodePort`. De esta manera, ahora podemos acceder fácilmente a la interfaz web de Prometheus cuando el Pod esté listo:

```bash
minikube service prometheus-server-np
```

Esto abrirá una ventana del navegador con la interfaz web de Prometheus.

## Paso 2: Instalar Grafana

Al igual que con Prometheus, los gráficos oficiales de Helm del canal estable para Grafana han sido desaprobados. Los gráficos recomendados son los alojados por el repositorio de Gráficos Helm de la Comunidad de Grafana.

Como antes, comenzaremos añadiendo el repositorio a nuestra configuración de Helm:

```bash
helm repo add grafana https://grafana.github.io/helm-charts
```

A continuación, instalamos Grafana utilizando los gráficos proporcionados:

```bash
helm install grafana grafana/grafana
kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-np
```

De nuevo, dado que estamos utilizando Minikube, para acceder fácilmente a la interfaz web de Grafana, exponemos el servicio como un `NodePort`.

Nota: Grafana está protegida por contraseña de forma predeterminada. Para recuperar la contraseña del usuario administrador, podemos ejecutar el siguiente comando:

```bash
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

Ahora podemos cargar la interfaz web de Grafana utilizando el usuario admin y la contraseña recuperada:

```bash
minikube service grafana-np
```

## Paso 3: Configurar la Fuente de Datos de Prometheus en Grafana

Una vez que hayamos iniciado sesión en la interfaz de administración, es hora de configurar la Fuente de Datos de Prometheus.

Necesitamos dirigirnos a **Configuraciones > Fuentes de Datos** y agregar una nueva instancia de Prometheus.

La URL para nuestra instancia de Prometheus es el nombre del servicio http://prometheus-server:80.

## Paso 4: Configurar un Dashboard de Kubernetes

Para este artículo del blog, usaré el [siguiente dashboard de Grafana](https://grafana.com/grafana/dashboards/6417), pero puedes usar cualquier otro Dashboard. Incluso puedes crear el tuyo propio fácilmente, pero eso se cubrirá en otro artículo.

Nos dirigimos a **Crear (+) > Importar** para Importar a través de grafana.com y configuramos 6417 en el campo de id y hacemos clic en Cargar.

En la configuración del dashboard, necesitamos seleccionar la Fuente de Datos de Prometheus que creamos en el paso anterior.

Una vez que confirmemos el diálogo de Importar, seremos redirigidos al nuevo Dashboard.

## Kubernetes Cluster (Prometheus)

Si todo salió bien, podrás ver la información de tu clúster en el Dashboard.

