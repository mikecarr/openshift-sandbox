# OpenShift OC Commands Cheat Sheet

## Clean everything in project
```
oc delete all --all
```

## Create Project Teamplate

creates default template
```
oc adm create-bootstrap-project-template -o yaml > template.yaml
```

Edit

Load the Teamplate
```
oc create -f template.yaml -n default
```

## Docker Registry Logs
```
oc logs dc/docker-registry -n default
```

## Cluster Status
```
oc status
oc get all -n default
```

## List Pods in Default Namespace
```
oc get pods -n default
```

## Restart Error Pods

List POD's
```
oc get pods
```

Delete ones in error
```
oc delete pod docker-registry-1-deploy
oc delete pod router-1-deploy
```

Get List of deployment configs
```
oc get dc
```

Roll out new POD's
```
oc rollout latest "docker-registry"
oc rollout latest "router"
```

Verify
```
oc get pods
```

### ConfigMaps
If you make some changes in deployment config and save them, pod will restart and and your changes will take effect:

```
oc edit dc "deploy-config-example"
```

If you change something in volumes or configmaps you need to delete pod for his restart:
```
oc delete pod "name-of-your-pod"
```

And pod will restart. Or better still trigger a new deployment by running:
```
oc rollout latest "deploy-config-example"
```

Using oc rollout is better because it will re-deploy all pods if you have a scaled application, and you don't need to identify each pod and delete it.
