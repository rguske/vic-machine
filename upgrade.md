## `vic-machine upgrade` the version of (an) existing Virtual Container Hosts to a newer version.

I wrote a blog post about the upgrade procedure: [Upgrade vSphere Integrated Containers](https://rguske.github.io/post/upgrade-vsphere-integrated-containers)

*Use `vic-machine ls` to get the needed vm-id for your Virtual Container Host.*

> *Please adjust the environment parameters accordingly to yours!*

```
./vic-machine-darwin upgrade \
--id vm-1190 \
--target lab-vcsa67-001.lab.jarvis.local/Datacenter-North \
--user administrator@jarvis.local \
--timeout 5m \
--force
```