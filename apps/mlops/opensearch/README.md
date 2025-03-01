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

# Installation de Minikube, Kubectl et Helm avec Ansible

Ce projet permet d'installer Minikube, Kubectl, et Helm sur une machine cible via un playbook Ansible, puis de déployer OpenSearch sur un cluster Kubernetes local.

## Prérequis

Avant d'exécuter le playbook, assure-toi que tu as les éléments suivants :

- Une machine de contrôle avec **Ansible** installé.
- Une machine cible avec un accès SSH configuré.
- Un fichier d'inventaire **inventory.ini** contenant les informations de connexion à la machine cible.

## Étapes pour exécuter le playbook

### 1. Vérifier si Ansible est installé

Sur ta machine de contrôle, vérifie si Ansible est installé avec la commande suivante :

```bash
ansible --version

---

Si Ansible n'est pas installé, tu peux l'installer avec cette commande :

```bash
sudo apt update && sudo apt install ansible -y
```

---

### 2. Créer un fichier d’inventaire

Crée un fichier nommé inventory.ini avec l'adresse IP ou le nom d'hôte de la machine cible, ainsi que les informations nécessaires pour l'accès SSH. Voici un exemple :


```bash
[servers]
your_server_ip ansible_ssh_user=your_user ansible_ssh_private_key_file=your_key.pem
```
---

1-Remplace your_server_ip par l'adresse IP de ton serveur.

2-Remplace your_user par ton utilisateur SSH.

3-Ajoute ta clé privée SSH si nécessaire.

---

![Capture d’écran 2025-01-29 214512](https://github.com/user-attachments/assets/640e5d9e-c378-49b7-98db-12f3fdc30ce2)

![Capture d’écran 2025-01-29 223315](https://github.com/user-attachments/assets/1ab67c91-d014-48e1-800d-b24c9e1d540b)

---

### 3. Créer un playbook install_minikube_kubectl_helm.yml

```bash 
sudo nano install_minikube_kubectl_helm.yml
```
--- et copier ce code dans ce fichier 

```bash
---
- name: Install Minikube, Kubectl, and Helm
  hosts: all
  become: yes
  tasks:
    - name: Update package lists
      apt:
        update_cache: yes

    - name: Download Minikube
      get_url:
        url: https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
        dest: /tmp/minikube-linux-amd64
        mode: '0755'

    - name: Install Minikube
      command: sudo install /tmp/minikube-linux-amd64 /usr/local/bin/minikube

    - name: Download Kubectl
      shell: curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
      args:
        chdir: /tmp

    - name: Make Kubectl executable
      file:
        path: /tmp/kubectl
        mode: '0755'

    - name: Move Kubectl to /usr/local/bin
      command: sudo mv /tmp/kubectl /usr/local/bin/

    - name: Verify Kubectl installation
      command: kubectl version --client
      register: kubectl_version

    - debug:
        msg: "Kubectl Version: {{ kubectl_version.stdout }}"

    - name: Install Helm
      shell: curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

    - name: Verify Helm installation
      command: helm version
      register: helm_version

    - debug:
        msg: "Helm Version: {{ helm_version.stdout }}"

    - name: Add OpenSearch Helm repository
      command: helm repo add opensearch https://opensearch-project.github.io/helm-charts/

    - name: Update Helm repositories
      command: helm repo update

    - name: Search for OpenSearch chart
      command: helm search repo opensearch
      register: opensearch_search

    - debug:
        msg: "Available OpenSearch charts: {{ opensearch_search.stdout }}"

    - name: Install OpenSearch with Helm
      command: helm install my-deployment opensearch/opensearch
```

---

![Capture d’écran 2025-01-29 224827](https://github.com/user-attachments/assets/1363a9db-4e6e-4ae5-b22b-396ebd380450)

---

### 4.Exécuter le Playbook

Pour lancer le playbook et installer Minikube, Kubectl, et Helm sur la machine cible, exécute la commande suivante :

```bash
ansible-playbook -i inventory.ini install_minikube_kubectl_helm.yml
```

Cette commande va exécuter les tâches définies dans le playbook et installer les outils nécessaires.

---

![image](https://github.com/user-attachments/assets/4c7c3ad9-6391-4806-92aa-dceb74a8db35)

---

### 5.Vérifier les installations
Après l'exécution du playbook, vérifie que les outils ont bien été installés en exécutant ces commandes sur la machine cible :

```bash
kubectl version --client
helm version
minikube version
```

![image](https://github.com/user-attachments/assets/e10d8b28-8767-4961-b6d9-b18bd0ba1e7d)





![Capture d’écran 2025-01-26 004018](https://github.com/user-attachments/assets/ae3b3ce7-54a2-4dbd-93e3-16d3b387c817)

---

![Capture d’écran 2025-01-26 011509](https://github.com/user-attachments/assets/f2150b7f-801c-405b-8747-5e02f0601159)
