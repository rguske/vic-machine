## `vic-machine update` the Firewall on an ESXi Host for the communication with the VCH.

> *Please adjust the environment parameters accordingly to yours!*

```
./vic-machine-darwin update firewall \
--target lab-vcsa67-001/Datacenter-North \
--user administrator@jarvis.local \
--compute-resource 192.168.178.70 \
--thumbprint  4F:D3:9B:50:00:31:D9:84:9D:DA:CF:57:21:D6:0D:11:89:78:97:26 \
--allow
```
