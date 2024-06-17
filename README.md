
---
## Helm
  - Instlación de la página oficial [Helm](https://helm.sh/es/docs/intro/install/)
  - Comandos de [Helm](https://helm.sh/es/docs/intro/cheatsheet/)
    
# Instalación de Jenkins en Minikube usando Helm

## Paso 1: Instalar Helm

Para instalar Helm en Windows, vamos a utilizar Chocolatey, un gestor de paquetes para Windows. Sigue estos pasos:

### 1. Instalar Chocolatey

Abre PowerShell como administrador y ejecuta el siguiente comando para instalar Chocolatey:

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

### 2. Instalar Helm con Chocolatey

Una vez que Chocolatey esté instalado, ejecuta el siguiente comando para instalar Helm:

```powershell
choco install kubernetes-helm
```

### 3. Verificar la instalación de Helm

Para verificar que Helm se ha instalado correctamente, ejecuta el siguiente comando:

```powershell
helm version
```

## Paso 2: Añadir el repositorio de Jenkins Helm

Para que Helm pueda descargar los archivos de configuración de Jenkins, necesitamos agregar el repositorio de Jenkins Helm. Ejecuta los siguientes comandos:

```bash
helm repo add jenkins https://charts.jenkins.io
helm repo update
```

- `helm repo add jenkins https://charts.jenkins.io`: Agrega el repositorio de Jenkins Helm con el nombre `jenkins`.
- `helm repo update`: Actualiza la lista de repositorios de Helm para asegurarnos de que tengamos la última versión del repositorio de Jenkins.

## Paso 3: Instalar Jenkins

Ahora que hemos agregado el repositorio de Jenkins, podemos instalar Jenkins en nuestro clúster de Kubernetes. Ejecuta el siguiente comando:

```bash
helm install jenkins jenkins/jenkins
```

Este comando instala Jenkins en el clúster de Kubernetes con el nombre de lanzamiento `jenkins`.

## Paso 4: Exponer el Servicio de Jenkins

Para acceder a Jenkins desde un navegador web, necesitamos exponer el servicio de Jenkins. Ejecuta el siguiente comando:

```bash
kubectl expose service jenkins --type=NodePort --target-port=8080 --name=jenkins-np
```

Este comando crea un servicio de tipo NodePort para Jenkins, lo que significa que será accesible desde fuera del clúster de Kubernetes a través de un puerto específico.

## Paso 5: Obtener la URL de Jenkins

Para obtener la URL de Jenkins y poder acceder a la interfaz gráfica de usuario, ejecuta el siguiente comando:

```bash
minikube service jenkins-np
```

Este comando abrirá Jenkins en tu navegador web predeterminado.

## Paso 6: Obtener la Contraseña de Administrador de Jenkins

La contraseña de administrador de Jenkins se almacena como un secreto en Kubernetes. Para obtener la contraseña, ejecuta el siguiente comando:

```bash
kubectl get secret --namespace default jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode && echo
```

Este comando decodificará y mostrará la contraseña de administrador de Jenkins.

## Paso 7: Iniciar Sesión en Jenkins

1. Abre la URL de Jenkins que obtuviste con el comando `minikube service jenkins-np`.
2. Usa `admin` como nombre de usuario.
3. Ingresa la contraseña que recuperaste en el paso anterior.

Siguiendo estos pasos, deberías poder instalar y acceder a Jenkins en tu clúster de Minikube.

--- 

Este README proporciona una guía detallada y completa para instalar Jenkins en Minikube, incluyendo la instalación de Helm y explicaciones detalladas de cada paso. Si necesitas más ayuda, no dudes en preguntar.
