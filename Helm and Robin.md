# Robin-Notes
| Kubernetes Command | Description |
| --- | ----------- |
|robin login [username] --password [password]|To login into robin cluster|
|robin login [username] --namespace|To login into a definite namespace|
|||
|||
|||
|robin bundle  add [given-name] [given-version] [filepath of bundle at server]| This command is used to add bundle in the cluster |
|robin bundle list| To get the list of all available bundles| 
|  robin bundle remove zoneid bundleid --force --yes| To remove bundle|
|robin  bundle open [bundle_id]| To edit the robin bundle|
|robin bundle close bundleid --commit new_version| To close the bundle after modification |
|robin app list|To get list of all the apps|
|robin app create from-bundle [app_name] [bundle_id]  --rpool [rpool_name]| It is for creating the application, here rpool may be deafult|
|robin rpool list|To get list o resouce pool|
|robin app remove app_name --force --yes| To remove app|
# Helm-Notes
| Kubernetes Command | Description |
| --- | ----------- |
|helm delete [releasename] -n [namespace]|To delete the daemon set |
|||
|helm create [NAME]|Create a default chart with the given name|
|helm dependencies build|To recompile the given helm chart|
|helm install [NAME] [CHART]|Install the given helm chart into K8s cluster|
|helm upgrade [NAME] [CHART]|Upgrades a specified release to a new version of a chart|
|helm history [NAME]	|Display historical revisions for a given release|
|helm rollback [NAME] [REVISION]|Roll back a release to a previous revision|
|helm uninstall [NAME]|Uninstall all of the resources associated with a given release|
|helm template [NAME] [CHART]|Render chart templates locally along with the values|
|helm list|Lists all of the helm releases inside a K8s cluster|
|helm get manifest [Chart-Name] |To get the manifest info which will have all the info related to chart |
|helm uninstall releasename --no-hooks --kubeconfig config| it is for uninstalling with no hooks|
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
#### Helm is package manager for k8s like pip for python. 
