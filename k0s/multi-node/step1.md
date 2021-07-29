First get the latest release of k0s:

`curl -sSLf get.k0s.sh | sudo sh`{{execute}}

Once this is done, check the current version of the k0s binary:

`k0s version`{{execute}}

You should get an output similar to the following one (your version could be slightly different though)

```
v1.21.3+k0s.1
```

First, install k0s as a controller node:

`sudo k0s install controller`{{execute}}

This create a k0scontroller systemd service.

Start this service:

`sudo k0s start`{{execute}}

Next, after a few seconds, verify it has been started properly:

`sudo k0s status`{{execute}}

You should should get an output similar the following one:

```
Version: v1.21.3+k0s.0
Process ID: 1343
Parent Process ID: 1
Role: controller+worker
Init System: linux-systemd
Service file: /etc/systemd/system/k0scontroller.service
```

As k0s comes with its own kubectl subcommand, you can directly list the status of our single node cluster:

`sudo k0s kubectl get node`{{execute}}

Note: as the current node is a controller node only it will not be listed. You will get the following output instead.

```
No resources found
```

In the next step you will add a worker node to the cluster.

