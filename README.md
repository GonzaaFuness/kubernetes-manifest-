Proyecto Kubernetes

Requisitos Previos
Antes de comenzar, asegurate de tener instaladas las siguientes herramientas en tu equipo:

Git: Para clonar el repositorio y gestionar versiones.

Minikube: Permite levantar un clúster local de Kubernetes.

Kubectl: Herramienta de línea de comandos para interactuar con el clúster.

Docker: Necesario para construir y correr contenedores.

Guía de Implementación
1. Clonar el Repositorio
Primero, obtené el proyecto desde GitHub. Este incluye tanto los archivos de la página como los manifiestos de Kubernetes necesarios para su despliegue:


Copiar
Editar
git clone https://github.com/GonzaaFuness/kubernetes-manifest-.git
2. Iniciar Minikube
Una vez clonado el repositorio, arrancá el clúster local ejecutando:


Copiar
Editar
minikube start
3. Montar la Carpeta al Pod
Necesitás montar la carpeta del proyecto al entorno de Minikube. En una terminal aparte (que deberás mantener abierta mientras Minikube esté en uso), ejecutá:


Copiar
Editar
minikube mount "Ruta local del proyecto clonado":/mnt/web
Reemplazá "Ruta local del proyecto clonado" con el path donde descargaste el repositorio.

4. Aplicar los Manifiestos
Ubicate en la carpeta donde están los archivos YAML y ejecutá los siguientes comandos en este orden:


Copiar
Editar
kubectl apply -f volumen/pv.yaml
kubectl apply -f volumen/pvc.yaml
kubectl apply -f desplegar/web-deployment.yaml
kubectl apply -f desplegar/web-deployment-direct.yaml
kubectl apply -f servicio/web-service.yaml
5. Verificar el Nombre del Pod
Para poder ingresar al pod y verificar los archivos montados, necesitás saber su nombre. Obtenelo con:


Copiar
Editar
kubectl get pods
6. Ingresar al Pod y Comprobar Archivos
Accedé al pod utilizando su nombre completo:

bash
Copiar
Editar
kubectl exec -it NOMBRE_DEL_POD -- /bin/sh
Por ejemplo: kubectl exec -it web-deployment-669985dbf7-4tlfj -- /bin/sh

Una vez dentro, listá los archivos del directorio donde deberían estar montados:


Copiar
Editar
ls -l /usr/share/nginx/html
Deberías ver archivos como index.html, style.css y la carpeta assets.

Para salir del pod, simplemente escribí:


Copiar
Editar
exit
7. Acceder a la Página Web
Finalmente, abrí el servicio en tu navegador con el siguiente comando:


Copiar
Editar
minikube service web-service
Esto abrirá una ventana del navegador con el sitio web funcionando desde el clúster.
