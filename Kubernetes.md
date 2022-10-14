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
|kubectl scale deployment accounts-deployment --replicas=3|To increase the number of replicas for a deployment inside your cluster **Unexpectedly --replicas is not wroking**|
|kubectl autoscale deployment **Name-of-deployment** --min=3 --max=10 --cpu-percent=70|To create automatic scaling using HPA for a deployment inside your cluster|
|kubectl rollout history deployment **Name-of-deployment**|To know the rollout history for a deployment inside your cluster|
|kubectl rollout undo deployment **Name-of-deployment** --to-revision=1|To rollback to a given revision for a deployment inside your cluster|
| kubectl logs [App-NAme] -f|For following the logs of application|
|kubectl proxy --port 8080| It will redirect all the API present in the cluster to the localhost:8080|
|kubectl api-resources|It is meant for showing all the resources available in the cluster|
|kubectl explain [pod/configmap/replicaset| It will give explaination about that service or reference|
|kubectl run nginx --image=nginx --port=80 --dry-run=client -o yaml| for getting the yaml file demo version, we can use it. Here, the dry-run=client will not create any resourse instead, it is used for testing purpose|
| kubectl get pods -l env=dev| It will filter all the pods which will have label named as env and has value as dev|
|kubectl get pods  --show-labels| To get the list of pods along with the labels |
|kubectl label pod [pod-name] [label key value] | It is for assigning label to any specific pod|
|kubectl label  pods --all status=running| To get the info about all the pods which has status as running|
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
 https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.25/#-strong-api-overview-strong-
 https://kubernetes.io/docs/reference/kubernetes-api/
 https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md
For creating yaml files, https://kubernetes.io/docs/concepts/workloads/pods/
Here, the ETCD will be storing information related to all the resources and kube API server is working as the single point of contact between all the k8s objects. 
![image](https://user-images.githubusercontent.com/38420375/195338708-a4e944d0-b2f0-4634-b7b0-ce63ee01d8f3.png)

https://kubernetes.io/docs/reference/kubectl/cheatsheet/ 

### Service is meant to route the traffic to the nodes as the nodes will have dynamic IPs(Due to auto-creation or self healing). Labels in the deployment is meant to get identified by Service, hence it should exactly mentioned inside the service.  

[Kubernetes.pdf](https://github.com/shivam005/Important-Notes/files/9433563/Kubernetes.pdf)

