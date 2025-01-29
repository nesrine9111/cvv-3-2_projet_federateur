# Exécution d'un Workflow Exemple avec Airflow sur Minikube
 
## 1. Créer un DAG Simple
 
Dans le dossier `dags/` de ton déploiement Airflow, ajoute un fichier `example_dag.py` :
 
```python
from airflow import DAG
from airflow.operators.dummy import DummyOperator
from datetime import datetime
 
default_args = {
    'owner': 'airflow',
    'start_date': datetime(2023, 1, 1),
}
 
with DAG('example_dag',
         default_args=default_args,
         schedule_interval='@daily',
         catchup=False) as dag:
 
    start_task = DummyOperator(task_id='start')
    end_task = DummyOperator(task_id='end')
 
    start_task >> end_task
```
 
## 2. Copier et Déployer le Fichier
 
Si ton pod Airflow a un volume monté, place directement le fichier dans ce volume sous `/opt/airflow/dags`. Sinon, utilise la commande suivante :
 
```bash
kubectl cp example_dag.py <nom_du_pod_airflow>:/opt/airflow/dags
```
 
## 3. Vérifier le DAG sur l'Interface Web
 
1. Accède à l'interface web d'Airflow (en supposant que le port `8080` soit exposé) :
   ```bash
   minikube service <nom_du_service_airflow> --url
   ```
 
2. Active le DAG `example_dag` dans l'interface.
 
## 4. Exécuter le DAG
 
Clique sur **Trigger DAG** pour lancer une exécution manuelle.
 
---
