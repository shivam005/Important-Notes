# Kubernetes-Notes

| Kubernetes Command | Description |
| --- | ----------- |
|  kubectl apply -f filename -n namespace | To create a deployment/service/configmap based on a given YAML file |
|kubectl get all | To get all the components inside your cluster|
|kubectl describe pod pod-id|To get more details of a given pod id|
|kubectl get pod pod-id|To get the details of a given pod id|
|kubectl delete pod pod-id|To delete a given pod from cluster |
|kubectl get services|To get all the services details inside your cluster|
|kubectl get events --sort-by=.metadata.creationTimestamp|To get all the events occured inside your cluster|
|kubectl scale deployment accounts-deployment --replicas=3  or  kubectl scale replicaset new-replica-set --replicas=5 |To increase the number of replicas for a deployment inside your cluster **Unexpectedly --replicas is not wroking**|
|kubectl autoscale deployment **Name-of-deployment** --min=3 --max=10 --cpu-percent=70|To create automatic scaling using HPA for a deployment inside your cluster|
|kubectl set image deployment [Name of deployment] nginx=nginx:1.16.1| It is for changing the image in the deployment, In this case image is being updated from nginx to nginx1.16.1|
|kubectl set image deployment [Name of deployment] nginx=nginx:1.16.1 --record|Here the --record plays very imp role by saving the command internally which will shown to us when we will run kubectl rollout history deployment [name of deployment] |
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
|systemctl||
|Taint and Toleration| Taint is for allowing a node to repel a set of pods. If taint has been applied to any node then only those pod which will have toleration with same value|
|kubectl config view| It is for checking the current context|
|kubectl config set-context --current --nameOfAttiribute toBeUpdatedValue| for changing any attribute of context|
|kubectl get sa|It is for fetching the service account which is responsible for athenticating client in the API server. It consist of secrets or token which is used by client. It we dont specify SA then a default SA is taken.|
|kubectl config get-contexts| It is getting info related to the currect context. Context refers to the default information available to be used by kubectl while communicating with the server |
|kubectl config set-context [name of context]| it is for setting the context|
|kubectl config --kubeconfig=base-config set-cluster development --server=https://1.2.3.4| for creating kubeconfig with the cluster detail|
|kubectl config --kubeconfig=base-config set-credentials experimenter --username=dev --password=some-password|for adding user detail in the config|
|kubectl get pv| to fetch the list of persistent volumes|
|kubectl get pvc| to fetch the list of persistent volume claim. |
|PV and PVC |In kubernetes, we just have got to define the pvc inside the pod and on the basis of configuration which has been demanded in PVC, a PV will be allocated automatically which will have sufficient resources to fullfill the demand of PVC. If in case, none of the PV matches the requirement then an PV will get created dynamically. |
|kubectl get configmap| configmap is like application.properties which can be mounted in pod like volumes and can be replaced as per our convenience or we can also directly make changes in the configmap without affecting the pod. | 
|Security-context| It is for specifying the access privilege of any pod as it is dangerous to have root access. it may be of three type runasuser, runasgroup, fsgroup. fsgroup applies the context to the volume path, runasuser applies to the current user and runasGroup applies to primary group of all the services within the group. |
|nodeSelector:   disktype: ssd | Under the (spec:) section of yaml, we can put this label and our pod will be deployed in only that node which will have this label. Make sure that disktype=ssd label has already been defined at the time of node creation  https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/ |
| https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/ |Node Affinity is similar to Node-Selector, It is also more flexible. Node Selector has also been depricated, so its better to use it. It has two types of checks preferredDuringSchedulingIgnoredDuringExecution(Soft check), requiredDuringSchedulingIgnoredDuringExecution(Hard check) |
|resource request and limit |Request and Limit are the upper and the lower bound for the resource assignment in the given pod. It specifies that the given pod will not work in the node which has less capacity than request. https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/|
|Pod affinity and antiaffinity |Node affinity allows you to schedule a pod on a set of nodes based on labels present on the nodes. However, in certain scenarios, we might want to schedule certain pods together or we might want to make sure that certain pods are never scheduled together. This can be achieved by PodAffinity and/or PodAntiAffinity respectively. https://github.com/infracloudio/kubernetes-scheduling-examples|
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
|https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-getting-started-strong-| It has list commands of kubectl api|


 https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.25/#-strong-api-overview-strong-
 https://kubernetes.io/docs/reference/kubernetes-api/
 https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md
 https://github.com/zealvora/certified-kubernetes-administrator
For creating yaml files, https://kubernetes.io/docs/concepts/workloads/pods/
Here, the ETCD will be storing information related to all the resources and kube API server is working as the single point of contact between all the k8s objects. 
![image](https://user-images.githubusercontent.com/38420375/195338708-a4e944d0-b2f0-4634-b7b0-ce63ee01d8f3.png)

https://kubernetes.io/docs/reference/kubectl/cheatsheet/ 

### Service is meant to route the traffic to the nodes as the nodes will have dynamic IPs(Due to auto-creation or self healing). Labels in the deployment is meant to get identified by Service, hence it should exactly mentioned inside the service.  

[Kubernetes.pdf](https://github.com/shivam005/Important-Notes/files/9433563/Kubernetes.pdf)

