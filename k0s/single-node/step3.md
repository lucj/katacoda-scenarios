## A quick word on k0s configuration

When running a k0s cluster, the default configuration is used unless another options  be used but it is also possible to modify that one to better match specific needs.

Check the content of the defaults configuration:

`k0s default-config`{{execute}}

To override some of those properties you can save the output in a file

`k0s default-config > k0s.config`{{execute}}

When you have modified the configuration file to match your needs,you just need to specify it, using the *-c* flag, when running k0s.

For instance, add the following entry in the list of sans (under .spec.api.sans), we will use that URL to access the cluster from the outside in a later step.

`https://[[HOST_SUBDOMAIN]]-6443-[[KATACODA_HOST]].environments.katacoda.com`

To restart the cluster taking into account this new configuration, you first need to stop the cluster

`sudo k0s stop`{{execute}}

Then you need to reset k0s removing all its related components: 

`sudo k0s reset`{{execute}}

Reinstall the cluster with its new configuration:

`sudo k0s install controller --single -c k0s.config`{{execute}}

The cluster can then be restarted, it will then take into account the configuration options specified

`sudo k0s start`{{execute}}