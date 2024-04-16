## Kubernetes Project Documentation

This documentation provides instructions for deploying a Kubernetes project composed of MongoDB and a MongoExpress web application using Minikube.

### Project Overview

The project consists of the following components:

- **MongoDB Deployment**: MongoDB is deployed using a Deployment and exposed via a Service.
- **Web Application Deployment**: A web application (MongoExpress) using MongoDB as its database, deployed using a Deployment and exposed via a Service.

### Prerequisites

Before you begin, ensure you have the following installed:

- Minikube
- kubectl
- Docker (optional, required only if you want to build Docker images)

### Steps to Deploy (Ubuntu)

1. **Start Minikube**

    ```bash
    minikube start --driver=docker
    ```

2. **Apply Kubernetes Manifests**

    Apply the Kubernetes manifest files in the following order:

    ```bash
    kubectl apply -f secret.yaml
    kubectl apply -f mongo-config.yaml
    kubectl apply -f mongo-app.yaml
    kubectl apply -f web-app.yaml
    ```

### Verification

To verify that the deployment was successful, you can use the following commands:

1. **Check Deployments**

    ```bash
    kubectl get deployments
    ```

2. **Check Services**

    ```bash
    kubectl get services
    ```

3. **Access Web Application**

    Get the Minikube IP address:

    ```bash
    minikube ip
    ```

    ```bash
    minikube service webapp-service
    ```

    Open a web browser and navigate to `http://<minikube-ip>:30200` to access the web application.

### Cleanup

To delete the deployed resources, you can use the following command:

```bash
kubectl delete deployment webapp-deployment
kubectl delete service webapp-service
kubectl delete secret mongo-secret
kubectl delete configmap mongo-config
kubectl delete deployment mongo-deployment
kubectl delete service mongo-service
```

### Note

- **Secrets**: Ensure that your sensitive data in the secrets (`mongo-secret`) is properly encoded (base64).
- **Configuration**: The MongoDB URL in the config map (`mongo-config`) should match the service name (`mongo-service`).
- **Networking**: Ensure that Minikube is running and accessible before deploying the project.
