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

## Deploy with config file (apply)

kubectl apply -f nginx-deployment.yaml

## Build mock image

`docker build -t mock:1.0.0 . -f ./mock/Dockerfile`

## REF

You can follow [kubectl cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
