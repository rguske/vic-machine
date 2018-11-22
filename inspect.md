## `vic-machine inspect` an existing Virtual Container Host to get for example the **Docker environment variables** or the **Docker endpoint data** listed.

> *Please beare in mind that the following example(s) are all based on my homelab parameters*

```
./vic-machine-darwin inspect \
--name vch-yelb \
--target lab-vcsa67-001.lab.jarvis.local/Datacenter-South \
--user adm.jarvis@LAB.JARVIS.LOCAL \
--thumbprint 4F:D3:9B:50:00:31:D9:84:9D:DA:CF:57:21:D6:0D:11:89:78:97:26
```