# Kubernetes-Notes

| Kubernetes Command | Description |
| --- | ----------- |
|  kubectl apply -f filename | To create a deployment/service/configmap based on a given YAML file |
|kubectl get all | To get all the components inside your cluster|
|kubectl describe pod pod-id|To get more details of a given pod id|
|kubectl get pod pod-id|To get the details of a given pod id|
|kubectl delete pod pod-id|To delete a given pod from cluster |
|kubectl get services|To get all the services details inside your cluster|
|kubectl get events --sort-by=.metadata.creationTimestamp|To get all the events occured inside your cluster|
|kubectl scale deployment accounts-deployment --replicas=3|To increase the number of replicas for a deployment inside your cluster|
|kubectl autoscale deployment **Name-of-deployment** --min=3 --max=10 --cpu-percent=70|To create automatic scaling using HPA for a deployment inside your cluster|
|kubectl rollout history deployment **Name-of-deployment**|To know the rollout history for a deployment inside your cluster|
|kubectl rollout undo deployment **Name-of-deployment** --to-revision=1|To rollback to a given revision for a deployment inside your cluster|
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
|||
||| 
|||
|||
|||
|||
