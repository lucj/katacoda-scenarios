## Install k0s

Run the following command to create a single node k0s cluster:

```
$ sudo k0s install controller --single
```

You should get an output similar to the following one:

```
INFO[2021-06-24 18:36:26] no config file given, using defaults         
INFO[2021-06-24 18:36:26] creating user: etcd                          
INFO[2021-06-24 18:36:26] creating user: kube-apiserver                
INFO[2021-06-24 18:36:26] creating user: konnectivity-server           
INFO[2021-06-24 18:36:26] creating user: kube-scheduler                
INFO[2021-06-24 18:36:26] Installing k0s service
```

🔥 if you need to provide some configuration options different from the default ones, you could provide a configuration file through the -c flag in the command above.

As you can see from this output, a k0s systemd service is created (but is not started yet)

## Start the cluster

First, start the cluster with the following command:

```
$ sudo k0s start
```

Next verify it has been started properly using the status subcommand:

```
$ sudo k0s status
```

You should should get an output similar the following one:

```
Version: v1.21.2+k0s.0
Process ID: 1672
Parent Process ID: 1
Role: controller+worker
Init System: linux-systemd
Service file: /etc/systemd/system/k0scontroller.service
```

It takes a few tens of seconds for the cluster to be up and running. 

As k0s comes with its own kubectl subcommand, you can directly list the status of our single node using the following command:

```
$ sudo k0s kubectl get node
```

You should get an output similar to the following one (the name of your node will be different though):

```
NAME              STATUS   ROLES    AGE     VERSION
ip-172-31-17-54   Ready    <none>   5m45s   v1.21.2+k0s
```
