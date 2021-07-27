In this part, you will create a single k0s cluster

First get the latest release of k0s:

```
curl -sSLf get.k0s.sh | sudo sh
```

After a few tens of seconds the k0s binary will be available in your PATH (in /usr/local/bin).

Next check the current version of the k0s binary:

```
k0s version
```

You should get an output similar to the following one (your version could be slightly different though)

```
v1.21.2+k0s.1

