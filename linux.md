Install on linux (Ubuntu)

=== Unuable to assisgn IP
https://docs.okd.io/latest/minishift/getting-started/quickstart.html

```
minishift addons enable admin-user
minishift ip --set-dhcp

```

https://medium.com/@maheshacharya_44641/install-openshift-origin-on-ubuntu-18-04-7b98773c2ee6
oc cluster up --skip-registry-check=true

output
```
not working either
```

working
https://www.techrepublic.com/article/how-to-install-openshift-origin-on-ubuntu-18-04/

NOTE: I don't think I copied kubectl to /usr/local/bin in the second attempt above.

## Starting
```
oc cluster up --public-hostname=SERVER_IP
```

