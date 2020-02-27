This Readme will help to build the Tekton pipeline

https://itnext.io/explore-different-methods-to-build-and-push-image-to-private-registry-with-tekton-pipelines-5cad9dec1ddc

### Create Secret

```shell
kubectl create secret docker-registry regcred --docker-server=quay.io/nicolaso/frontend --docker-username=XXXXXXX --docker-password=XXXXXXX --docker-email=XXXXXX
```
### Troubeshoot

tkn pipeline start build-and-deploy
tkn pipelinerun logs build-and-deploy-run-z2rz8 -f -n pipelines-tutorial

```shell
tkn pipeline ls
tkn resource ls
tkn pipeline logs -f
```

If you want to re-run the pipeline again, you can use the following short-hand command to rerun the last pipelinerun again that uses the same pipeline resources and service account used in the previous pipeline run:

```shell
tkn pipeline start build-and-deploy --last
```


```shell
oc adm policy add-cluster-role-to-user cluster-admin -z socks-shop
```
### Socks shop pods also need to run as priviliaged containers, so grant 'priviliged' Security Context Constrains (SCC) for 'socks-shop' service account

```shell
oc adm policy add-scc-to-user privileged -z socks-shop
```
### Socks app has an init daemon that has to run as UID 0, so grant 'anyuid' SCC for 'default' service account

```shell
oc adm policy add-scc-to-user anyuid -z default
```
### Deploy application in OpenShift using oc tools

```shell
oc create -f complete-demo.yaml
```
OR
```shell
oc create -f https://raw.githubusercontent.com/NicolasO/microservices-demo/master/deploy/openshift/complete-demo.yaml
```


### Expose the Front end Service :

```shell
oc expose service front-end
```


### to delete application in OpenShift using oc tools

```shell
oc delete -f complete-demo.yaml
```
OR
```shell
oc delete -f https://raw.githubusercontent.com/NicolasO/microservices-demo/master/deploy/openshift/complete-demo.yaml
```
