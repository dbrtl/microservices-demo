This deployment has been tested on OCP 4.3.

### Create a dedicated project for socks shop then apply policy changes needed to run socks shop:

```shell
oc new-project sock-shop
```
### Socks shop pods need full access to Kubernetes API via 'socks-shop' service account

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
oc apply -f complete-demo.yaml
```
OR
```shell
oc apply -f https://raw.githubusercontent.com/NicolasO/microservices-demo/master/deploy/openshift/complete-demo.yaml
```


### Expose the Front end Service :

```shell
oc expose service front-end
```
