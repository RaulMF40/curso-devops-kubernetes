echo "# Mi Proyecto" > README.md
1 ejercicio: necesitamos crear un pod que contenga MYSQL.
comprobar que existe el pod, eliminarlo, ver si está o no, etc.

- resolución del 1º. (luego lo pasamos a yaml)
  apiVersion: v1
  kind: Pod
  metadata:
  name: pod-mysql
  spec:
  containers: - name: mysql
  image: mysql:latest
  env: - name: MYSQL_ROOT_PASSWORD
  value: 'raulmoyaclase'

---

2 ejercicio: necesitamos tener al menos 3 pods que cada uno de ellos tenga: MYSQL, UBUNTU y una app hello-world
comprobar que existen, eliminar uno, mirar el yaml de otro,
entrar en la terminal del tercero

- resolución 2º. (luego lo pasamos a yaml si hay que camb iar algo)
  apiVersion: v1
  kind: Pod
  metadata:
  name: mysql-pod
  spec:
  containers: - name: mysql
  image: mysql:5.7
  env: - name: MYSQL_ROOT_PASSWORD
  value: rootpassword

---

apiVersion: v1
kind: Pod
metadata:
name: ubuntu-pod
spec:
containers: - name: ubuntu
image: ubuntu:latest
command: - sleep - '3600'

---

apiVersion: v1
kind: Pod
metadata:
name: hello-world-pod
spec:
containers: - name: hello-world
image: strm/helloworld-http
ports: - containerPort: 80

3 ejercicio necesitamos tener un pod que contenga al menos 4 replicas.
eliminar uno y ver que ocurre.
-resolucion del tercero

---

apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
spec:
replicas: 4
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers: - name: nginx
image: nginx:alpine
env: - name: MY_VARIABLE
value: raul - name: OTRA_VARIABLE
value: raulmoya
resources:
requests:
memory: 64Mi
limits:
memory: 128Mi
readinessProbe:
httpGet:
path: /
port: 80
initialDelaySeconds: 5
periodSeconds: 10
livenessProbe:
tcpSocket:
port: 80
initialDelaySeconds: 60
periodSeconds: 10
ports: - containerPort: 80

---

kind mas importantes que veremos
-pod - unidad minima
-deployment-desplegar aplicaciones y gestiona las replicas
-Statefulset: para mantener el estado d elas apps
-daemonset: monitoreo
-service. permite exponer nuestras apps tanto externamente como internamente
-configmap - variables de entorno
-secret - para mantener secretos

- ingress - (es el que más se utiliza), nos permite gestionar el trafico
-

y otros kind menos importantes
-replicaSet - asegura un numero minimo de replicas
-job - ejecuta una unica tarea
-cronjob: ejecucion periodica de algo
-persistenvolume - proporciona almacenamiento a los pods
-persistenVolumenclain
-networkpolicy - reglas de red en pods
-horizontalpodautoescaler - ajusta automaticamente el numero de pods
-namespace - crea un namespace
-limitrange - definir limites minimos y maximos de los pods de un namespace
-resourcequote - limita la cantidad de recusos por un namespace

ME HE QUEDADO EN 28 MINUTOS
