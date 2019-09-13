#  Minishift


## Starting
```
minishift start
```

## Stopping
```
minishift stop
```

## Deleting (erasing completely) OpenShift
```
minishift delete
NOTE: Windows these folders are under the Admin user home folder
rm -rf ~/.minishift
rm -rf ~/.kube
```

## Windows Specific

* Open Command Windows as Admin
* External VM Switch

Starting
```
minishift config set hyperv-virtual-switch "External VM Switch"
minishift start --memory=2GB
```

should see

<i>1st time running</i>
```

```