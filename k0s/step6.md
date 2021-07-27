## Cleanup

In order to remove k0s from the VM (without deleting the VM) you first need to stop k0s:

```
$ sudo k0s stop
```

and then to use the reset command:

```
$ sudo k0s reset
```

You will get an output similar to the following one, indicating all the k0s related components have been removed:

```
INFO[2021-06-24 19:05:43] * containers steps                           
INFO[2021-06-24 19:05:50] successfully removed k0s containers!         
INFO[2021-06-24 19:05:50] no config file given, using defaults         
INFO[2021-06-24 19:05:50] * remove k0s users step:                     
INFO[2021-06-24 19:05:50] no config file given, using defaults         
INFO[2021-06-24 19:05:50] * uninstal service step                      
INFO[2021-06-24 19:05:50] Uninstalling the k0s service                 
INFO[2021-06-24 19:05:50] * remove directories step                    
INFO[2021-06-24 19:05:56] * CNI leftovers cleanup step                 
INFO k0s cleanup operations done. To ensure a full reset, a node reboot is recommended. 
```

