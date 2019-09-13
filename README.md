# openshift-sandbox
My personal notes while learning OpenShift



## CI/CD

### References
* https://blog.sonatype.com/nexus-in-openshift

## Application Deployment

SpringBoot

```
oc new-app wildfly:10.0~https://github.com/mikecarr/spring-boot-employee-webservice

oc expose svc spring-boot-employee-webservice

```


## Commands

Add cluster-admin role to user
```
oc adm policy --as system:admin add-cluster-role-to-user cluster-admin developer
```



## References
* https://github.com/cesarvr/Spring-Boot
