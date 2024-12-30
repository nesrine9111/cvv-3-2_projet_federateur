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

Pour plus de variables consultez ce lien:
https://github.com/apache/airflow/blob/main/chart/values.yaml#L285
