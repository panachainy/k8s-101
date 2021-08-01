# K8S-101

## Pre-requisite

* Homebrew
* macOS
* Basic docker knowledge

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

https://kubernetes.io/docs/reference/kubectl/cheatsheet/

> you can use flag --watch for watching some change of kube for see current result.

## [Lesson 1] How to check Deployment and Service is correct

```sh
kubectl describe service/nginx-service
# Name:              nginx-service
# Namespace:         default
# Labels:            <none>
# Annotations:       <none>
# Selector:          app=nginx
# Type:              ClusterIP
# IP:                10.110.200.138
# Port:              <unset>  80/TCP
# TargetPort:        80/TCP
# Endpoints:         172.17.0.3:80,172.17.0.4:80
# Session Affinity:  None
# Events:            <none>
```

```sh
kubectl get pod -o wide
# NAME                                READY   STATUS    RESTARTS   AGE    IP           NODE       NOMINATED NODE   READINESS GATES
# nginx-deployment-644599b9c9-f9qsh   1/1     Running   0          9m3s   172.17.0.3   minikube   <none>           <none>
# nginx-deployment-644599b9c9-hhv7q   1/1     Running   0          9m1s   172.17.0.4   minikube   <none>           <none>
```

Check at `Endpoints` on service is match to `IP` of pods.

## [Lesson 2]

Create namespace

   ```sh
   # Config file way
   kubectl apply -f ./lesson-2/mongo-namespace.yaml

   #or

   # CLI way
   kubectl create namespace mongo
   ```

Create all k8s config file under folder lesson-2

   ```sh
   kubectl apply -f ./lesson-2 --namespace=mongo
   ```

### Load balance

Apply with `lesson-2/mongo-express.yaml`

```sh
kubectl get service
# NAME                    TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
# kubernetes              ClusterIP      10.96.0.1        <none>        443/TCP          19h
# mongo-express-service   LoadBalancer   10.101.207.134   <pending>     8081:30000/TCP   100m
# mongodb-service         ClusterIP      10.97.64.40      <none>        27017/TCP        3h2m
```

Open mongo-express-service

   `minikube service mongo-express-service`

### Change active namespaces

Install

`brew install kubectx`

`kubens`

`kubens <your-namespace>`

### Delete namespace

   ```sh
   # This deletes everything under the namespace!
   kubectl delete namespaces mongo
   ```

## Lesson 3

### Prerequire

#### Dashboard

For try to set ingress to dashboard

Open k8s dashboard

   `minikube dashboard`

### Setup Ingress controller for minikube

`minikube addons enable ingress`

> Set this if you can't enable ingress `minikube start --vm=true --driver=hyperkit`

ref: https://github.com/kubernetes/minikube/issues/7332

### Setting Host for local

sudo vim /etc/hosts

```txt
127.0.0.1      localhost
192.168.64.5   dashboard.com
```

this way work `lesson-3/old-version-dashboard-ingress.yaml`

### Log level of kubectl

| Verbosity | Description                                                                                                               |
| --------- | ------------------------------------------------------------------------------------------------------------------------- |
| --v=0     | Generally useful for this to always be visible to a cluster operator.                                                     |
| --v=1     | A reasonable default log level if you don't want verbosity.                                                               |
| --v=2     | Useful steady state information about the service and important log messages that may correlate to significant changes in | the | system. This is the recommended default log level for most systems. |
| --v=3     | Extended information about changes.                                                                                       |
| --v=4     | Debug level verbosity.                                                                                                    |
| --v=5     | Trace level verbosity.                                                                                                    |
| --v=6     | Display requested resources.                                                                                              |
| --v=7     | Display HTTP request headers.                                                                                             |
| --v=8     | Display HTTP request contents.                                                                                            |
| --v=9     | Display HTTP request contents without truncation of contents.                                                             |

ref: https://kubernetes.io/docs/reference/kubectl/cheatsheet/

## REF

You can follow [kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

[Kubernetes Tutorial for Beginners](https://www.youtube.com/watch?v=X48VuDVv0do)
