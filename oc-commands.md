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
``

Delete ones in error
```
oc delete pod docker-registry-1-deploy
oc delete pod router-1-deploy
```

Get List of deployment configs
```
oc get dc
``

Roll out new POD's
```
oc rollout latest "docker-registry"
oc rollout latest "router"
```

Verify
```
oc get pods
```
