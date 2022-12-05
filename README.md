# dist-for-lulz

This is a simple project to learn about different distributed systems and manage them using kubernetes.

# Initial setup

- Install `minikube`
- Install `kubectl`
- Install `helm`
- Start a new minikube profile by running:
```
minikube start -p mid --cpus=4 --disk-size='20000mb' --memory='8g' --mount=true --mount-string=$HOME/dev/minikubemount:/minikube/common
```
Note: You can replace `$HOME/dev/minikubemount` with any directory in your host machine. This is to provide a way to make development and testing easy in the apiServer deployment.

- Set the new profile as default
```
minikube profile mid
```

- Set kubectl to your minikube kubectl version to avoid mismatch of kubernetes and kubectl versions
```
alias kubectl="minikube kubectl --"
```

Tip: You can add the alias to your `.zshrc` (or your preferred shell profile)

# Components in the system

The distributed system contains the following components:
- postgres
- redis
- kafka
- apiServer (A simple Go application)

# Deploying the system on minikube

## Build helm dependencies

```
cd helm/distforlulz
helm dep build
```

## Install the helm chart

```
cd helm/disforlulz
helm install distforlulz .
```

## Wait for all your K8s pods to run successfully

```
kubectl get pods
```

```
NAME                                    READY   STATUS    RESTARTS      AGE
distforlulz-apiserver-8956fc64d-wzrh6   1/1     Running   0             13m
distforlulz-kafka-0                     1/1     Running   1 (13m ago)   13m
distforlulz-postgresql-0                1/1     Running   0             13m
distforlulz-redis-master-0              1/1     Running   0             13m
distforlulz-redis-replicas-0            1/1     Running   0             13m
distforlulz-redis-replicas-1            1/1     Running   0             13m
distforlulz-redis-replicas-2            1/1     Running   0             12m
distforlulz-zookeeper-0                 1/1     Running   0             13m
```
