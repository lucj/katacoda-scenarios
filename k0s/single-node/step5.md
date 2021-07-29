## Communication from an external machine

Usually, we do not ssh into a controller node to manage the cluster but use an external machine instead. In this part, you will communicate with the cluster (the one running on Katacoda) from your own machine.

First retrieve the kubeconfig file generated during the cluster creation, this one is in */var/lib/k0s/pki/admin.conf*.

`sudo cat /var/lib/k0s/pki/admin.conf > ./kubeconfig`{{execute}}

As this kubeconfig references an API Server on localhost, you need to replace `localhost:6443` with the URL added as  an additional SAN (Subject Alternative Name) in the step 3.

Note: you can use Katacoda's editor for that purpose

In the kubeconfig file, change the following part

```
clusters:
- cluster:
    server: https://localhost:6443
    ...
```

into

```
clusters:
- cluster:
    server: https://[[HOST_SUBDOMAIN]]-6443-[[KATACODA_HOST]].environments.katacoda.com
    ...
```

Copy this new version of the kubeconfig file on your local machine.

## Kubectl

Install kubectl on your machine, this can be easily done following the instructions from [https://kubernetes.io/docs/tasks/tools/#kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl)

Then setup the KUBECONFIG environment variable so it contains the path towards the kubeconfig file you've just downloaded.

You can then access the cluster from your local machine:

`kubectl get no`{{execute}}

Note: currently got the following error that needs to be fixed:
```
Unable to connect to the server: x509: certificate signed by unknown authority
```