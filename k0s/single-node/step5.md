## Communication from an external machine

Usually, we do not ssh into a controller node to manage the cluster but use an external machine instead. In this part, you will setup the admin machine to communicate with the cluster.

First retrieve the kubeconfig file generated during the cluster creation, this one is in */var/lib/k0s/pki/admin.conf*.

`sudo cat /var/lib/k0s/pki/admin.conf > ./kubeconfig`{{execute}}

As this kubeconfig references an API Server on localhost, you need to replace `localhost:6443` with the URL added as  an additional SAN (Subject Alternative Name) in the step 3.

In the  kubeconfig file, the following part

```
clusters:
- cluster:
    server: https://localhost:6443
    ...
```

should then look like:

```
clusters:
- cluster:
    server: https://[[HOST_SUBDOMAIN]]-6443-[[KATACODA_HOST]].environments.katacoda.com
    ...
```

Copy this new version of the kubeconfig file on your local machine.
