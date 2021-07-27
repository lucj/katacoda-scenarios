## Running a sample workload

Let's now run a Deployment based on the ghost image (ghost is an open source blogging platform) and expose it though a NodePort Service.

`cat<<EOF | sudo k0s kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ghost
spec:
  selector:
    matchLabels:
      app: ghost
  template:
    metadata:
      labels:
        app: ghost
    spec:
      containers:
      - name: ghost
        image: ghost
        ports:
        - containerPort: 2368
---
apiVersion: v1
kind: Service
metadata:
  name: ghost
spec:
  selector:
    app: ghost
  type: NodePort
  ports:
  - port: 2368
    targetPort: 2368
    nodePort: 30000
EOF`{{execute}}

Make sure the resources have been created correctly:

`sudo k0s kubectl get deploy,po,svc`{{execute}}

You should get an output similar to the following one (some identifiers might be different though)

```
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/ghost   0/1     1            0           11s

NAME                         READY   STATUS              RESTARTS   AGE
pod/ghost-548879c755-x2m6d   0/1     ContainerCreating   0          11s

NAME                 TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
service/kubernetes   ClusterIP   10.96.0.1      <none>        443/TCP          14m
service/ghost        NodePort    10.100.70.91   <none>        2368:30000/TCP   11s
```

The Ghost interface should now be accessible from port 30000.
