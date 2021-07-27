## Default k0s configuration

When running a k0s cluster, the default configuration options can be used but it is also possible to modify that one to better match specific needs.

The following command shows the defaults configuration:

```
$ k0s default-config
apiVersion: k0s.k0sproject.io/v1beta1
kind: Cluster
metadata:
  name: k0s
spec:
  api:
    address: 192.168.64.48
    port: 6443
    k0sApiPort: 9443
    sans:
    - 192.168.64.48
  storage:
    type: etcd
    etcd:
      peerAddress: 192.168.64.48
  network:
    podCIDR: 10.244.0.0/16
    serviceCIDR: 10.96.0.0/12
    provider: kuberouter
    calico: null
    kuberouter:
      mtu: 0
      peerRouterIPs: ""
      peerRouterASNs: ""
      autoMTU: true
    kubeProxy:
      disabled: false
      mode: iptables
  podSecurityPolicy:
    defaultPolicy: 00-k0s-privileged
  telemetry:
    enabled: true
  installConfig:
    users:
      etcdUser: etcd
      kineUser: kube-apiserver
      konnectivityUser: konnectivity-server
      kubeAPIserverUser: kube-apiserver
      kubeSchedulerUser: kube-scheduler
  images:
    konnectivity:
      image: us.gcr.io/k8s-artifacts-prod/kas-network-proxy/proxy-agent
      version: v0.0.20
    metricsserver:
      image: gcr.io/k8s-staging-metrics-server/metrics-server
      version: v0.3.7
    kubeproxy:
      image: k8s.gcr.io/kube-proxy
      version: v1.21.2
    coredns:
      image: docker.io/coredns/coredns
      version: 1.7.0
    calico:
      cni:
        image: docker.io/calico/cni
        version: v3.18.1
      node:
        image: docker.io/calico/node
        version: v3.18.1
      kubecontrollers:
        image: docker.io/calico/kube-controllers
        version: v3.18.1
    kuberouter:
      cni:
        image: docker.io/cloudnativelabs/kube-router
        version: v1.2.1
      cniInstaller:
        image: quay.io/k0sproject/cni-node
        version: 0.1.0
    default_pull_policy: IfNotPresent
  konnectivity:
    agentPort: 8132
    adminPort: 8133
```

🔥 to override some of those properties you can save the output of the previous command in a file, modify that one to match our needs and then use it when running k0s (more on that below)
