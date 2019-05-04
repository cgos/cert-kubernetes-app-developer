# K8s Object

| K8s Object                        | Command                                                                                          |
|-----------------------------------|--------------------------------------------------------------------------------------------------|
| List all k8s objects              | kubectl api-resources -o name                                                                    |
| List system pods                  | kubectl get pods -n kube-system                                                                  |
| Overview of an objectCluster info | kubectl cluster-info dump                                                                        |
| View the nodes in the cluster     | kubectl get nodes                                                                                |
| Create a secret                   | kubectl create secret generic db-user-pass --from-file=./username.txt --from-file=./password.txt |
| Create service account            | kubectl create serviceaccount my-serviceaccount                                                  |
|                                   |                                                                                                  |

# Pod

# Namespace

# Deployment