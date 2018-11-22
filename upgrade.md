## `vic-machine upgrade` the version of (an) existing Virtual Container Host(s) to a newer version.

How to: <a href="https://rguske.github.io/post/upgrade-vsphere-integrated-containers/" target="_blank">Upgrade vSphere Integrated Containers</a>

*Use `vic-machine` ls to get the needed vm-id´s for your Virtual Container Hosts.*

```
./vic-machine-darwin upgrade \
--id vm-1190 \
--target lab-vcsa67-001.lab.jarvis.local/Datacenter-North \
--user administrator@jarvis.local \
--timeout 5m \
--force
```