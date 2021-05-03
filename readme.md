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

## REF

You can follow [kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
