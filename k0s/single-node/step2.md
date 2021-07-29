In this step you will start k0s in the single-node configuration.

Create a single node k0s cluster:

`sudo k0s install controller --single`{{execute}}

You should get an output similar to the following one:

```
INFO[2021-06-24 18:36:26] no config file given, using defaults         
INFO[2021-06-24 18:36:26] creating user: etcd                          
INFO[2021-06-24 18:36:26] creating user: kube-apiserver                
INFO[2021-06-24 18:36:26] creating user: konnectivity-server           
INFO[2021-06-24 18:36:26] creating user: kube-scheduler                
INFO[2021-06-24 18:36:26] Installing k0s service
```

This output shows that k0s systemd service is created (but is not started yet).

You can get additional information using systemctl:

`sudo systemctl status k0scontroller`{{execute}}

Start the cluster:

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

Note: it takes a few tens of seconds for the cluster to be up and running, for a few tens of seconds you might get the following output:

```
No resources found
```

When the cluster is up and running you should get an output similar to the following one (the name of your node will be different though):

```
NAME     STATUS   ROLES    AGE   VERSION
host01   Ready    <none>   53s   v1.21.3+k0s
```
