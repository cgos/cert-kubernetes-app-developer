Notes and snippets for the Certified Kubernetes Application Developer courses

# Core Concepts
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
|                                      |                                                        |