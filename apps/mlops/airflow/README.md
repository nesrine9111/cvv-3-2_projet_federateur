# Installation de Minikube et Airflow sous Minikube

## 📦 Pré-requis
1. **Système d'exploitation** : Linux/Windows/macOS.
2. **Logiciels nécessaires** :
   - Minikube
   - Kubectl
   - Docker

---

## 🚀 Étapes d'installation

### 1. Installer Minikube
- Téléchargez Minikube :
  ```bash
  curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
  sudo install minikube-linux-amd64 /usr/local/bin/minikube
## Lancez Minikube 
  minikube start

---

### 2. Installer Apache Airflow sous Minikube  
```
  kubectl create namespace airflow
  helm repo add apache-airflow https://airflow.apache.org
  helm repo update
  helm install airflow apache-airflow/airflow --namespace airflow
  kubectl port-forward svc/airflow-webserver 8080:8080 -n airflow
```
 - Ouvrez votre navigateur : 
   http://localhost:8080

 - Ou remplacer localhost par l'ip du cluster qui permet l'accès au service ainsi au pod contenant l'application airflow

---

### 3. les variables dans values.yaml 
 - On peut personnaliser les valeurs par défaut de la chart helm de airflow à travers le fichier values.yaml.
 - les variables qu'on peut personnaliser:
```
# Provide a name to substitute for the full names of resources
fullnameOverride: ""
# Provide a name to substitute for the name of the chart
nameOverride: ""
# Max number of old replicasets to retain. Can be overridden by each deployment's revisionHistoryLimit
revisionHistoryLimit: ~
# Global container lifecycle hooks for airflow containers
containerLifecycleHooks: {}

# Airflow home directory
# Used for mount paths
airflowHome: /opt/airflow

# Default airflow repository -- overridden by all the specific images below
defaultAirflowRepository: apache/airflow
# Airflow version (Used to make some decisions based on Airflow Version being deployed)
airflowVersion: "2.10.4"

# Images
images:
  airflow:
    repository: ~
    tag: ~

# Select certain nodes for airflow pods.
nodeSelector: {}
affinity: {}
tolerations: []
topologySpreadConstraints: []
schedulerName: ~

# Add common labels to all objects and pods defined in this chart.
labels: {}

# Ingress configuration
ingress:
  # Enable all ingress resources (deprecated - use ingress.web.enabled and ingress.flower.enabled)
  enabled: ~

  # Configs for the Ingress of the web Service
  web:
    # Enable web ingress resource
    enabled: false

    # The path for the web Ingress
    path: "/"

    tls:
      # Enable TLS termination for the web Ingress
      enabled: false
      # the name of a pre-created Secret containing a TLS private key and certificate
      secretName: ""
# Network policy configuration
networkPolicies:
  # Enabled network policies
  enabled: false
# Volumes for all airflow containers
volumes: []

# VolumeMounts for all airflow containers
volumeMounts: []

# Secrets for all airflow containers
secret: []
# - envName: ""
#   secretName: ""
#   secretKey: ""
```
La commande qu'on peut utiliser pour lancer la chart en personnalisant les variables à travares le fichier values.yaml est la suivante:
```
helm install airflow apache-airflow/airflow --values values.yaml
```
Pour plus de variables consultez ce lien:
https://github.com/apache/airflow/blob/main/chart/values.yaml#L285

---

### 4- L'argument --set
- Vous pouvez personnaliser des variables spécifiques sans utiliser l'argument --value mais en utilisant --set et ne spécifier que l'essentiel comme montre l'exemple suivant:
```
helm install airflow apache-airflow/airflow \   --set airflow.executor=CeleryExecutor,workers.replicas=3
```
 
#### A. airflow.executor=CeleryExecutor : 
  - Dans Apache Airflow, l'executor est responsable de la gestion de l'exécution des tâches. Airflow prend en charge différents types d'executors en fonction de l'échelle et de l'infrastructure.
  - CeleryExecutor :
    Cet executor est conçu pour l'exécution distribuée des tâches.
    Il utilise Celery, une file d'attente de tâches distribuée, pour gérer l'exécution des tâches sur plusieurs nœuds de travail (workers).
    Utile pour exécuter des workflows à grande échelle où les tâches doivent être distribuées sur plusieurs machines.
    Nécessite un broker de messages (comme RabbitMQ ou Redis) et un backend pour les résultats (comme une base de données).
    Si vous exécutez Airflow dans un cluster Kubernetes et que vous avez besoin d'une exécution distribuée, le CeleryExecutor est souvent préféré à l'executor par défaut, comme SequentialExecutor ou LocalExecutor.
#### B. workers.replicas=3 :
  - Cette configuration est spécifique au Helm chart pour Apache Airflow.
    workers.replicas :
    Définit le nombre de pods worker Airflow qui seront créés dans le cluster Kubernetes.
    Les workers sont les entités responsables de l'exécution des tâches dans vos workflows (DAGs).
    En définissant workers.replicas=3, cela signifie que 3 pods worker seront créés pour gérer les tâches.

#### C. Exemple d'utilisation :
   - Si vous utilisez le CeleryExecutor et que vous prévoyez d'exécuter plusieurs tâches simultanément, vous pouvez définir workers.replicas=3 pour avoir 3 pods worker traitant les tâches en parallèle. Ensemble, l'executor et le paramètre des réplicas permettent une exécution des tâches distribuée et évolutive.
---
