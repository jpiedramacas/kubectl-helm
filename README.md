

## Paso 1: Añadir el repositorio de Jenkins Helm

```bash
helm repo add jenkins https://charts.jenkins.io
helm repo update
```

## Paso 2: Instalar Jenkins

```bash
helm install jenkins jenkins/jenkins
```

## Paso 3: Exponer el Servicio de Jenkins

```bash
kubectl expose service jenkins --type=NodePort --target-port=8080 --name=jenkins-np
```

## Paso 4: Obtener la URL de Jenkins

```bash
minikube service jenkins-np
```

## Paso 5: Obtener la Contraseña de Administrador de Jenkins

```bash
kubectl get secret --namespace default jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode && echo
```

Este comando decodificará y mostrará la contraseña de administrador de Jenkins.

## Paso 6: Iniciar Sesión en Jenkins

1. Abre la URL de Jenkins que obtuviste con `minikube service jenkins-np`.
2. Usa `admin` como nombre de usuario.
3. Ingresa la contraseña que recuperaste en el paso anterior.

Siguiendo estos pasos, deberías poder instalar y acceder a Jenkins en tu clúster de Minikube.
