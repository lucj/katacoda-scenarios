In this step, you will download and installed the k0s binary

First get the latest release of k0s:

`curl -sSLf get.k0s.sh | sudo sh`{{execute}}

After a few tens of seconds the k0s binary will be available in your PATH (in /usr/local/bin).

Next check the current version of the k0s binary:

`k0s version`{{execute}}

You should get an output similar to the following one (your version could be slightly different though)

```
v1.21.2+k0s.1
```
