In this step you will add a worker node in the cluster

First get the join token from the controlplane node:

`sudo k0s token create --role=worker > ./worker_token`{{execute}}

Note: the *worker* role specified in the command indicates that the token will be used to add a worker (that is the default value). We could also use a *controller* role to add additional controllers in the cluster.

Next copy that token into node01, in */tmp/worker_token*. You might need to switch to the fullscreen view to get the whole token as this is a quite long string.

Next download k0s onto node01:

`curl -sSLf get.k0s.sh | sudo sh`{{execute HOST2}}

Install it as a worker node providing the join token as a parameter:

`sudo k0s install worker --token-file /tmp/worker_token`{{execute HOST2}}

Then start it:

`sudo systemctl start k0sworker`{{execute HOST2}}

It will take a few tens of seconds to get the worker node ready. After it's running you can list the nodes from the controlplane:

`sudo k0s kubectl get node`{{execute}}

You should now be able to see the newly added worker:

```
NAME     STATUS   ROLES    AGE   VERSION
node01   Ready    <none>   32s   v1.21.3+k0s
```

Note: only the worker node appears in this list due to the control plane isolation feature of k0s.

You've succesfully created a multi-node cluster containing one controller and one worker node.