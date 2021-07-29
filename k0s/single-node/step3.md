## A quick word on k0s configuration

When running a k0s cluster, the default configuration is used unless another options be used but it is also possible to modify that one to better match specific needs. In this part, you will slightly change the configuration adding a new SAN (Subject Alternative Name).

First, check the content of the defaults configuration:

`k0s default-config`{{execute}}

To override some of those properties, save the configuration in a file:

`k0s default-config > k0s.config`{{execute}}

Add the following entry in the list of sans (under .spec.api.sans), you will use that URL to access the cluster from the outside in a later step.

`[[HOST_SUBDOMAIN]]-6443-[[KATACODA_HOST]].environments.katacoda.com`

To restart the cluster taking into account this new configuration, you first need to stop the cluster

`sudo k0s stop`{{execute}}

Then reset k0s removing all its related components: 

`sudo k0s reset`{{execute}}

and reinstall the cluster with its new configuration:

`sudo k0s install controller --single -c k0s.config`{{execute}}

The cluster can then be restarted, it will then take into account the configuration options specified

`sudo k0s start`{{execute}}

After a few tens of seconds the cluster will be up and running which you can verify by listing the node once again:

`sudo k0s kubectl get node`{{execute}}