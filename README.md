Notes and snippets for the Certified Kubernetes Application Developer courses

When using terminal in tmux
alias k=kubectl

tmux
split window: ctrl-b %
next window: ctrl-b n

# kubectl cheat sheet

Kubernetes objects

| K8s Object                        | Command                                           |
|-----------------------------------|---------------------------------------------------|
| List all k8s objects              | kubectl api-resources -o name                     |
| List system pods                  | kubectl get pods -n kube-system                   |
| Overview of an objectCluster info | kubectl cluster-info dump                         |
| View the nodes in the cluster     | kubectl get nodes                                 |
| Create serviceaccount             | kubectl create serviceaccount my-serviceaccount   |
| Get Service                       | kubectl get svc                                   |

Deployment object related command

| Deployment                        | Command                                                           |
|-----------------------------------|-------------------------------------------------------------------|
| List Deployments                  | kubectl get deployments                                           |
| Edit Deployment                   | kubectl edit deployment.v1.apps/nginx-deployment                  |
| View Deployment ReplicaSet        | kubectl get rs                                                    |
| View Deployment ReplicaSet        | kubectl rollout history deployment/rolling-deployment             |
| Rollback a Deployment             | kubectl rollout undo deployment/<deployment-name>                 |
| Rollback a Deployment             | kubectl rollout undo deployment/<deployment-name> --to-revision=X |

Pod object related command

| Pods                                 | Command                                                |
|--------------------------------------|--------------------------------------------------------|
| Create pod                           | kubectl create -f my-pod.yml                           |
| Create pod from image                | kubectl create deployment http --image=whateverimage   |
| Edit a running pod                   | kubectl edit pod my-pod -n <namespace>                 |
| See all running pod                  | kubectl get pods --all-namespaces                      |
| Check the state of a running pod     | kubectl describe pods my-pod                           |
| Apply new config on pod              | kubectl apply -f my-pod.yml                            |
| Delete pod                           | kubectl delete pod my-pod                              |
| Get pods from namespace              | kubectl get pods -n my-ns                              |
| Execute a command within a container | kubectl exec my-configmap-volume-pod -- ls /etc/config |
| See logs from pod                    | kubectl logs my-configmap-pod                          |
| Retrieve IP of a running pod         | kubectl get pod fruit-service -o=custom-columns=IP:.status.podIP --no-headers |
| View resource usage from pods        | kubectl top pods                                       |
| View resource usage from pods        | kubectl top pods -n my-namespace                       |


# Core Concepts

## Kubernetes primitives

K8s objects are building block of all running k8s application. [See understanding kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)


## Creating a pod

[See pod overview](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/)


To save and modify a the description of a running pod:
```
kubectl get pod <pod-name> -n <namespace> -o yaml --export > my-pod.yml
```

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

[See Resource requests and limits of Pod and Container](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/#resource-requests-and-limits-of-pod-and-container)

## Secrets

[See Secrets reference](https://kubernetes.io/docs/concepts/configuration/secret/)

## ServiceAccounts

[See managing service accounts](https://kubernetes.io/docs/reference/access-authn-authz/service-accounts-admin/)

[See configuring service accounts for pods](https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/)



# Multi-Container Pods

[See basic logging](https://kubernetes.io/docs/concepts/cluster-administration/logging/#using-a-sidecar-container-with-the-logging-agent)

[See communication between container within the same pod](https://kubernetes.io/docs/tasks/access-application-cluster/communicate-containers-same-pod-shared-volume/)

[See discussion around three patterns: sidecar, ambassador and adapter](https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/)

# Observability
## Liveness and Readiness Probes

[See pod lifecycle and container probes](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#container-probes)

[See how to configure liveness and readiness probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)

## Container Logging

[See the container logging architecture](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

Cluster-level logging requires a separate backend to store, analyze, and query logs.

## Monitoring Applications

[See resource monitoring and usage](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/)

## Debugging
How to find and fix broken pods

[See debug pods and replicationControllers](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-pod-replication-controller/)

[See debug service](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/)

[See tools for monitoring resources](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/)

If the
```
kubectl describe pods my-pod
```
shows the pod in Pending, it means there's probably insufficient resources preventing the pod to be scheduled onto a node
* Check node capacities
```
kubectl get nodes -o json
```

If the pod is in Waiting state, probably there's a failure pulling the image.
* Check image name is correct
* Check the image is in the repo
* Try a manual docker pull

If the pod is crashing, look at the logs or try executing a command in the pod.

# Pod Design
## Labels, Selectors and Annotations

[See labels and selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)

[See annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/)

Kubernetes labels provide a way to attach custom, identifying information to your objects. Selectors can then be used to filter objects using label data as criteria. Annotations, on the other hand, offer a more freeform way to attach useful but non-identifying metadata. In this lesson, we will discuss labels, selectors, and annotations. We will also demonstrate how to use them in a cluster.<Paste>

| Labels and selector                        | Command                                           |
|--------------------------------------------|---------------------------------------------------|
| List pods where env=prod and tier=frontend | kubectl get pods -l environment=production,tier=frontend|
| List pods where env label is prod or qa    | kubectl get pods -l 'environment in (production, qa)'|
| List pods where env label is not prod      | kubectl get pods -l 'environment notin (production)'|


 In contrast to lables, annotations are not used to identify and select objects.

## Deployments

[See deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
Deployment declares and manage a set of replica pods. A deployment defines a desired state for the pods for which the cluster will work to maintain that state.

## Rolling Updates and Rollbacks

[See section on updating and rolling back a deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
You can edit a running Deployment
```
kubectl edit deployment.v1.apps/nginx-deployment
```

## Jobs and CronJobs

[See Jon run to completion](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/)
[See CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/)
[See Running Automated Tasks with CronJob](https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/)

To list all the pods that belong to a Job in a machine readable form:
```
pods=$(kubectl get pods --selector=job-name=pi --output=jsonpath='{.items[*].metadata.name}')
echo $pods
```

# Services and Networking
## Services

[See Services](https://kubernetes.io/docs/concepts/services-networking/service/)
[See Using a Service to expose an app](https://kubernetes.io/docs/tutorials/kubernetes-basics/expose/expose-intro/)


Deployment manages a set of replica set of pods.

A Kubernetes Service is an abstraction which defines a logical set of Pods and a policy by which to access them - sometimes called a micro-service

There are 4 types of Service:
* ClusterIP
* NodePort
* LoadBalancer
* ExternalName

## NetworkPolicies

# State Persistence
## Volumes
## PersistenceVolumes and PersistentVolumeClaims

# Practice Exam

# Wrap-up
