# 📦 Déploiement de l’Example Voting App sur Kubernetes

Ce projet montre comment déployer l’application open-source [Example Voting App](https://github.com/dockersamples/example-voting-app) dans un cluster Kubernetes. Elle simule un système de vote distribué avec mise à jour en temps réel des résultats.

---

## 🧰 Prérequis

- Cluster Kubernetes fonctionnel (K3s)
- `kubectl` installé et configuré
- `git` installé

---

## 🖥️ Architecture

L’application est composée de plusieurs services :

- **vote** : interface web permettant de voter entre deux options
- **redis** : file d’attente pour stocker temporairement les votes
- **worker** : lit les votes depuis Redis et les écrit dans PostgreSQL
- **db** : base PostgreSQL persistante
- **result** : interface web affichant les résultats en temps réel

![image](https://github.com/user-attachments/assets/1d55ad93-e587-4b51-9d41-e8fedcbc00a7)


---

# Déploiement complet



# Clonage du dépôt
git clone https://github.com/dockersamples/example-voting-app.git
cd example-voting-app/k8s-specifications

![image](https://github.com/user-attachments/assets/33c684e5-8a9c-4470-9196-2877e374d75c)


# Création d'un namespace
kubectl create namespace voting-app

![image](https://github.com/user-attachments/assets/cf372968-c05d-4fce-8722-b07a0d9c98ce)

# Déploiement des services 
kubectl apply -f redis-deployment.yaml -n voting-app
kubectl apply -f redis-service.yaml -n voting-app
kubectl apply -f db-deployment.yaml -n voting-app
kubectl apply -f db-service.yaml -n voting-app

![image](https://github.com/user-attachments/assets/add0f0c4-c5a1-41ec-841c-7c6c928c70c4)


Lister les pods :

kubectl get pods -n voting-app

Lister les services :


kubectl get svc -n voting-app

Lister toutes les ressources :


kubectl get all -n voting-app

![image](https://github.com/user-attachments/assets/d194804b-8ab3-486d-b618-500ce9ffb5a5)

🌐 Accès à l’application
Récupérer l’IP d’un node :

kubectl get nodes -o wide

![image](https://github.com/user-attachments/assets/0ef03cd9-50af-42e7-8835-5b09cd95746e)

Accéder aux interfaces web :

Interface de vote : (http://172.180.0.59:31000/)

![image](https://github.com/user-attachments/assets/48c8058a-5b4c-4d35-a923-d5ac825fbb2c)


Interface des résultats : (http://172.180.0.59:31001/)

![image](https://github.com/user-attachments/assets/fcd848f4-9712-4a45-a447-6afaa4d12f2e)


✅ Résultat attendu
Les votes apparaissent en temps réel dans l’interface de résultats.

L’application fonctionne comme un système distribué complet.

🧼 Nettoyage
Pour supprimer toutes les ressources :
kubectl delete ns voting-app



