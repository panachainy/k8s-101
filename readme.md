# K8S-101

## Pre-requisite

* Homebrew
* macOS
* basic docker knowledge

## Setup

1. ทำการอัพเดท Homebrew

   ```bash
    brew update
   ```

2. ติดตั้ง minikube

   ```bash
    brew install minikube
   ```

   > kubectl จะติดตั้งไปพร้อมกับ minikube ไปด้วยเลยครับ

3. start minikube

   ```bash
    minikube start
   ```

## Command

// deploy

```bash
# try deploy with nginx
kubectl create deployment nginx-deploy --image=nginx
```

// check deploy

```bash
kubectl get deployment
# NAME           READY   UP-TO-DATE   AVAILABLE   AGE
# nginx-deploy   1/1     1            1           119s
```

// get pod

```bash
kubectl get pod
# NAME                           READY   STATUS    RESTARTS   AGE
# nginx-deploy-d4789f999-cpfcp   1/1     Running   0          3m48s
```

// get replicaset

```bash
kubectl get replicaset
# NAME                     DESIRED   CURRENT   READY   AGE
# nginx-deploy-d4789f999   1         1         1       5m23s
```

// edit deployment

kubectl edit deployment nginx-deploy

// check log

kubectl logs nginx-deploy-d4789f999-cpfcp

// describe

kubectl describe pod nginx-deploy-d4789f999-cpfcp

// shell

kubectl exec -it nginx-deploy-d4789f999-cpfcp -- bin/bash

// delete

kubectl delete deploy nginx-deploy

## Deploy with config file (apply)

kubectl apply -f nginx-deployment.yaml

## REF

You can follow [kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
