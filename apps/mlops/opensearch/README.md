## Cette partie est pour gérer les sources du sous-projet opensearch.
- [https://opensearch.org/](https://opensearch.org/)
- [https://github.com/opensearch-project/OpenSearch](https://github.com/opensearch-project/OpenSearch)

# contributeurs
- **AYADI NESRINE**
- **OMAR SFAXI**

  # Guide d'installation d'OpenSearch

OpenSearch est une plateforme collaborative et open-source de recherche et d'analyse, utilisée par les développeurs pour l'ingestion, la recherche, la visualisation et l'analyse des données.  
La plateforme comprend :  
- **Un moteur de recherche et de stockage de données** (OpenSearch)  
- **Un outil de visualisation et une interface utilisateur** (OpenSearch Dashboards)  
- **Un collecteur de données côté serveur** (Data Prepper)  

En outre, OpenSearch peut être enrichi grâce à une variété de plugins qui améliorent les fonctionnalités de recherche, d'analyse, d'observabilité, de sécurité, d'apprentissage automatique, et bien plus encore.

---

## Prérequis

Avant d'installer OpenSearch, assurez-vous d'avoir les éléments suivants :

---

- **Java** : OpenSearch nécessite Java 21 ou une version ultérieure. Installez Java si ce n'est pas déjà fait :
  ```bash
  sudo apt update
  sudo apt install openjdk-21-jdk -y
  ```
---

- **Minikube** : est un outil qui vous permet d'exécuter un cluster Kubernetes localement.

---

## Étapes d'installation

### 1. Installer Minikube

Téléchargez et installez `Minikube` en exécutant la commande suivante dans votre terminal :
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
---

### 2. Démarrer Minikube

Après l'installation, initialisez Minikube pour démarrer un cluster Kubernetes local :
```bash
minikube start
```
Cela lancera un cluster Kubernetes local avec un seul nœud. Vous pouvez maintenant déployer vos applications sur ce cluster.

![Capture d’écran 2025-01-25 211124](https://github.com/user-attachments/assets/9f0b481f-20e1-4c8a-a34f-52da93dc2f74)

---

-**kubectl** est l'outil CLI pour interagir avec Kubernetes.

---

## Étapes d'installation

### 1. Téléchargez kubectl :

Exécutez la commande suivante pour télécharger la version stable de `kubectl` :

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

### 2. Rendez-le exécutable et déplacez-le dans votre PATH:

Exécutez les commandes suivantes pour rendre le fichier exécutable et le déplacer dans un répertoire du PATH :

```bash
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

### 3. Vérifiez l'installation:

Exécutez la commande suivante pour vérifier que `kubectl` est bien installé:

```bash
kubectl version --client
```

![Capture d’écran 2025-01-25 213040](https://github.com/user-attachments/assets/14f8e4fc-7c90-4ecc-ad2e-449600a7d134)


---

- **Helm** : Helm est un gestionnaire de packages pour Kubernetes.

---

## Étapes d'installation:

---

### 1. Téléchargez le script d’installation de `Helm` :

Exécutez la commande suivante pour télécharger et installer `Helm` :

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

---

### 2. Vérifiez l'installation:

Exécutez la commande suivante pour vérifier que `Helm` est bien installé:

```bash
helm version 
```
![Capture d’écran 2025-01-25 213331](https://github.com/user-attachments/assets/3f1f1f58-9a5e-4e66-aaaa-2be80fcb61df)


---

# Installation d'OpenSearch avec Helm

Ce guide fournit les étapes nécessaires pour installer OpenSearch sur un cluster Kubernetes en utilisant Helm.

## Étape 1 : Ajouter le dépôt Helm d'OpenSearch

Pour installer OpenSearch via Helm, ajoutez d'abord le dépôt Helm des charts OpenSearch à votre configuration Helm.

```bash
helm repo add opensearch https://opensearch-project.github.io/helm-charts/
```

---

## Étape 2 : Mettre à jour les dépôts Helm

Mettez à jour vos dépôts `Helm` .

```bash
helm repo update
```

---

## Etape 3 : Recherche des charts Helm OpenSearch

Pour rechercher des charts Helm liés à OpenSearch, vous pouvez utiliser la commande suivante :

```bash
helm search repo opensearch
```

![Capture d’écran 2025-01-25 214318](https://github.com/user-attachments/assets/642eec64-22fd-44ef-84da-a4208100b485)

---

## Etape 4 : Déployer OpenSearch avec Helm

Pour déployer OpenSearch sur votre cluster Kubernetes, vous pouvez utiliser la commande suivante :

```bash
helm install mon-deploiement opensearch/opensearch
```
![Capture d’écran 2025-01-25 214318](https://github.com/user-attachments/assets/3f6ccce3-ab4d-4de7-8093-6f3ad0f71fd0)

![Capture d’écran 2025-01-25 214318](https://github.com/user-attachments/assets/ad7a792f-31eb-4065-82fb-51bb61431a96)


---

# Installation d'OpenSearch avec Docker

OpenSearch est une solution open-source pour la recherche et l'analyse des données. Cette section explique comment installer et exécuter rapidement OpenSearch avec Docker.

## Prérequis

- **Docker** installé sur votre système ([Documentation officielle](https://docs.docker.com/get-docker/)).
- Minimum 4 Go de mémoire disponible pour OpenSearch.

## Instructions

1- **Téléchargez les images de DOCKER HUB :**
   ```bash
   docker pull opensearchproject/opensearch:2
   docker pull opensearchproject/opensearch-dashboards:2
   ```

---

2. **Téléchargez et exécutez OpenSearch :**
   ```bash
    docker run -d -p 9200:9200 -p 9600:9600 -e "discovery.type=single-node" -e "OPENSEARCH_INITIAL_ADMIN_PASSWORD=<custom-admin-password>"    opensearchproject/opensearch:latest
   ```

---

![Capture d’écran 2025-01-25 234416](https://github.com/user-attachments/assets/2b3a9d29-22f6-4bf7-80c2-12f58839c045)

---

![Capture d’écran 2025-01-26 001511](https://github.com/user-attachments/assets/8dc3c311-416f-4250-b94b-c28126553a9d)

---

![Capture d’écran 2025-01-26 004018](https://github.com/user-attachments/assets/ae3b3ce7-54a2-4dbd-93e3-16d3b387c817)

---

![Capture d’écran 2025-01-26 011509](https://github.com/user-attachments/assets/f2150b7f-801c-405b-8747-5e02f0601159)
