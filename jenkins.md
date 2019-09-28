# Jenkins HelloWorld
## Docker install and Run
```
docker run \
  -u root \
  --rm \
  -d \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins-data:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkinsci/blueocean
```

### Post Install
https://jenkins.io/doc/book/installing/#setup-wizard

* Browse to http://localhost:8080

Search for admin password 
```
docker ps
docker logs
```

## References
* https://jenkins.io/doc/book/installing/#setup-wizard
