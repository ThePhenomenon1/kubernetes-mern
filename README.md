# MERN Dockerized Project with Kubernetes and Minikube

This project demonstrates a MERN application deployed using Kubernetes and orchestrated with Minikube. It includes MongoDB as the database and Mongo Express for database administration.

---

## Prerequisites

Ensure you have the following tools installed on your machine:

- [Docker](https://www.docker.com/get-started)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Git](https://git-scm.com/)

---

## Setup Instructions

### 1. Clone the Repository
Clone the project from GitHub:
bash
git clone https://github.com/ThePhenomenon1/kubernetes-mern.git
cd your-repo

### 2. Pull Necessary Docker Images

docker pull mongo:latest
docker pull mongo-express:latest

### 3. Generate Kubernetes Secrets

### Since secret.yaml is not included in the repository, you must generate the required secrets. Use the following steps:

Generate a random username and password using Python:

import secrets
print("mongo-user:", secrets.token_hex(12))
print("mongo-password:", secrets.token_hex(12))

Save these values for later use.

Create the Kubernetes Secret:

kubectl create secret generic mongo-secret \
  --from-literal=mongo-user=<your-generated-mongo-user> \
  --from-literal=mongo-password=<your-generated-mongo-password>

### 4. Configure Minikube

Start Minikube and set up your local Kubernetes cluster:

minikube start

Deploy the Application

### 1. Apply the Kubernetes manifests:

kubectl apply -f mongo-app.yaml
kubectl apply -f web-app.yaml

### 2. Verify the deployments:

kubectl get pods
kubectl get services

### 3. Access the application:

Forward the Mongo Express service to localhost:

kubectl port-forward svc/webapp-service 8081:8081

Open your browser and navigate to http://localhost:8081.

Notes

    The secret.yaml file is excluded from the repository for security reasons.
    Be sure to replace <your-generated-mongo-user> and <your-generated-mongo-password> with the values you generated.

Links

    Clone the Project: https://github.com/ThePhenomenon1/kubernetes-mern.git
    GitHub Repository: View on GitHub

License

This project is licensed under the MIT License.
