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

Ou remplacer localhost par l'ip du cluster qui permet l'accès au service ainsi au pod contenant l'application airflow
