## Communication from an external machine

Usually, we do not ssh into a controller node to manage the cluster but use an external machine instead. In this part, you will setup the admin machine to communicate with the cluster.

- On the *k0s* virtual machine

First retrieve the kubeconfig file generated during the cluster creation, this one is in */var/lib/k0s/pki/admin.conf*.

```
$ sudo cp /var/lib/k0s/pki/admin.conf > ./kubeconfig
```

As this kubeconfig references an API Server on localhost, you need to replace that value with the IP address of the VM. From the *Machine Info* menu, you can get all the information needed to access the *k0s* machine from the outside such as the external DNS name and the external IP.

ADD IMAGES HERE

Save the external IP address in the *NODE_IP* environment variable and replace localhost with that one:

```
sed -i '' "s/localhost/$NODE_IP/" ./kubeconfig
```

- On the *admin* machine

Install the *kubectl* binary with the following commands:

```
curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"

chmod +x ./kubectl

sudo mv ./kubectl /usr/local/bin/kubectl
```

Then configure your local kubectl so it uses this kubeconfig:

```
$ export KUBECONFIG=$PWD/kubeconfig
```

The local kubectl can now communicate with the newly created cluster. List the nodes to make sure this is working properly:

```
$ kubectl get nodes
NAME              STATUS   ROLES    AGE     VERSION
ip-172-31-17-54   Ready    <none>   7m51s   v1.21.2+k0s
```

