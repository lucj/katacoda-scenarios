In this step you will add a worker node in the cluster

First get the join token from the control plane node:

`sudo k0s token create --role=worker > ./worker_token`{{execute}}

Note: the *worker* role specified in the command indicates that the token will be used to add a worker (that is the default value). We could also use a *controller* role to add additional controllers in the cluster.

Next copy that token into Host2, in */tmp/worker_token* 

Next download k0s onto Host2

`curl -sSLf get.k0s.sh | sudo sh`{{execute HOST2}}

Install it as a worker node providing the join token as a parameter

`sudo k0s install worker --token-file /tmp/worker_token`{{execute HOST2}}

Then start k0s on Host2

`sudo systemctl start k0sworker`{{execute HOST2}}

List the cluster's nodes from Host1

`sudo k0s kubectl get node`{{execute HOST2}}

You should now be able to see the newly added worker:

```
$ kubectl get nodes
NAME     STATUS  ROLES    AGE     VERSION
host-2   Ready   <none>   1m20s   v1.21.3+k0s
```

Note: it can take a few tens of seconds for the node to appear in Ready status