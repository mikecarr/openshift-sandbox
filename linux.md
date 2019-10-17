Install on linux (Ubuntu)
<hr/>
=== Unuable to assisgn IP
https://docs.okd.io/latest/minishift/getting-started/quickstart.html

```
minishift addons enable admin-user
minishift ip --set-dhcp

```
<i>didnt work</i>

<hr/>
https://medium.com/@maheshacharya_44641/install-openshift-origin-on-ubuntu-18-04-7b98773c2ee6
oc cluster up --skip-registry-check=true

output
```

```

<i>didnt work</i>
<hr/>
<b>worked</b>

https://www.techrepublic.com/article/how-to-install-openshift-origin-on-ubuntu-18-04/

NOTE: I don't think I copied kubectl to /usr/local/bin in the second attempt above.


## Starting

First time starting
```
Login to server ...
Creating initial project "myproject" ...
Server Information ...
OpenShift server started.

The server is accessible via web console at:
    https://127.0.0.1:8443

You are logged in as:
    User:     developer
    Password: <any value>

To login as administrator:
    oc login -u system:admin
```

Edit


```
oc cluster up --public-hostname=SERVER_IP
oc cluster down
```

if you don't specify the public hostname above you can do it this was as well
```
cd ~/workspace/openshift 
sudo vi ./openshift.local.clusterup/openshift-controller-manager/openshift-master.kubeconfig
```


```
Server Information ...
OpenShift server started.

The server is accessible via web console at:
    https://10.0.1.79:8443
```

## Redirect caveat
If you find you keep getting redirected to https://127.0.0.1:8443, you can get around that by creating an SSH tunnel with the command:

<b>Add /console to the URL!<b>

```
sudo ssh -L 8443:localhost:8443 -f -N USER@SERVER_IP
```

Where USER is a remote username and SERVER_IP is the IP address on the hosting server. Now you should be able to point your browser to the Web GUI and not be constantly redirected to the localhost address.


## Ubuntu, SNAP and Docker
Well apparently I had docker installed via snap so I had two version fighting... see https://github.com/docker/for-linux/issues/660

to remove
```
sudo snap remove docker
```

When I ran docker info afer a restart
```
Client:
 Debug Mode: false

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 4
 Server Version: 18.06.1-ce
 Storage Driver: aufs
  Root Dir: /var/snap/docker/common/var-lib-docker/aufs
  Backing Filesystem: extfs
  Dirs: 7
  Dirperm1 Supported: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 468a545b9edcd5932818eb9de8e72413e616e86e
 runc version: N/A (expected: 69663f0bd4b60df09991c08812a60108003fa340)
 init version: 949e6fa (expected: fec3683)
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 4.15.0-62-generic
 Operating System: Ubuntu Core 16
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 7.692GiB
 Name: halcyon
 ID: ANPG:PTD7:LQVN:2U63:B6PZ:O5KT:IA7K:IM4K:NUKZ:KQT2:R6B5:OCLH
 Docker Root Dir: /var/snap/docker/common/var-lib-docker
 Debug Mode: true
  File Descriptors: 23
  Goroutines: 44
  System Time: 2019-09-14T17:12:02.55130428-07:00
  EventsListeners: 0
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false

WARNING: No swap limit support
```

docker-info after manuall restarting it
```
Client:
 Debug Mode: false

Server:
 Containers: 24
  Running: 0
  Paused: 0
  Stopped: 24
 Images: 12
 Server Version: 19.03.2
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 894b81a4b802e4eb2a91d1ce216b8817763c29fb
 runc version: 425e105d5a03fabd737a126ad93d62a9eeede87f
 init version: fec3683
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 4.15.0-62-generic
 Operating System: Ubuntu 18.04.3 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 4
 Total Memory: 7.692GiB
 Name: halcyon
 ID: Y37O:2TYR:2SGT:E44K:TJIH:UGAD:7SIU:YNYQ:ZYCG:2JTW:SRWU:3GKT
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  172.30.0.0/16
  127.0.0.0/8
 Live Restore Enabled: false

WARNING: API is accessible on http://0.0.0.0:2376 without encryption.
         Access to the remote API is equivalent to root access on the host. Refer
         to the 'Docker daemon attack surface' section in the documentation for
         more information: https://docs.docker.com/engine/security/security/#docker-daemon-attack-surface
WARNING: No swap limit support
```

## Hostname not resolveable

edit openshift.local.clusterup/kubedns/resolv.conf and add:
```
nameserver 8.8.8.8
```
