Notes and snippets for the Certified Kubernetes Application Developer courses

# Core Concepts

## Kubernetes primitives

K8s objects are building block of all running k8s application. [See understanding kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)

| K8s Object                        | Command                                                                                          |
|-----------------------------------|--------------------------------------------------------------------------------------------------|
| List all k8s objects              | kubectl api-resources -o name                                                                    |
| List system pods                  | kubectl get pods -n kube-system                                                                  |
| Overview of an objectCluster info | kubectl cluster-info dump                                                                        |
| View the nodes in the cluster     | kubectl get nodes                                                                                |

## Creating a pod

[See pod overview](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)

| K8s Object                           | Command                                                |
|--------------------------------------|--------------------------------------------------------|
| Create pod                           | kubectl create -f my-pod.yml                           |
| Create pod from image                | kubectl create deployment http --image=whateverimage   |
| Edit a running pod                   | kubectl edit pod my-pod                                |
| Apply new config on pod              | kubectl apply -f my-pod.yml                            |
| Delete pod                           | kubectl delete pod my-pod                              |
| Get pods from namespace              | kubectl get pods -n my-ns                              |
| Execute a command within a container | kubectl exec my-configmap-volume-pod -- ls /etc/config |
| See logs from pod                    | kubectl logs my-configmap-pod                          |

## Namespace

[See namespace overview](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)

| Namespace         | Command                 |
|-------------------|-------------------------|
| Get Namespaces    | kubectl get namespaces  |
| Create Namespaces | kubectl create ns my-ns |

## Basic Container Configuration

[See define a command and args for a container](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/)


| Container                     | Command                                                                                 |
|-------------------------------|-----------------------------------------------------------------------------------------|
| Expose container on port 8000 | kubectl expose deployment http --external-ip="172.17.0.16" --port=8000 --target-port=80 |
| Scale the http deployment     | kubectl scale --replicas=3 deployment http                                              |

# ConfigMaps

[See configure a pod to use a ConfigMap](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)

## SecurityContext

[See configure a security context for a pod or container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)

## Resouce Requirements
## Secrets
## ServiceAccounts

# Multi-Container Pods

# Observability
## Liveness and Readiness Probes
## Container Logging
## Installing Metrics Server
## Monitoring Applications
## Debugging

# Pod Design
## Labels, Selectors and Annotations
## Deployments
## Rolling Updates and Rollbacks
## Jobs and CronJobs


# Services and Networking
## Services
## NetworkPolicies

# State Persistence
## Volumes
## PersistenceVolumes and PersistentVolumeClaims

# Practice Exam

# Wrap-up
