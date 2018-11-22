## `vic-machine delete` a Virtual Container Host.

> *Please beare in mind that the following example(s) are all based on my homelab parameters*

```
./vic-machine-darwin delete \
--target lab-vcsa67-001/Datacenter-North \
--user administrator@jarvis.local \
--name vch01 \
--thumbprint=4F:D3:9B:50:00:31:D9:84:9D:DA:CF:57:21:D6:0D:11:89:78:97:26 \
--force
```