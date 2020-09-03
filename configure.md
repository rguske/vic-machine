## `vic-machine configure` gives you the ability to add a specific configuration like e.g. a dedicated network (Container Network) for your instantiated Container-VMs to your Virtual Container Host afterwards.

> *Please adjust the environment parameters accordingly to yours!*

Use `vic-machine ls` to get the needed vm-id´s for your Virtual Container Hosts. **Example:**

```
./vic-machine-linux ls --target vic@jarvis.lab@vcsa.jarvis.lab/Stark-Industries --thumbprint 55:AC:B3:2D:9B:56:62:F...

INFO[0000] vSphere password for vic@jarvis.lab:      
INFO[0003] ### Listing VCHs ####                        
INFO[0003] Validating target                            

ID              PATH                                           NAME        VERSION                      UPGRADE STATUS
vm-14989        /Stark-Industries/host/Malibu/Resources        mk5         v1.5.5-21324-50a44954        Up to date
```

### Add a ded. Container-Network to an existing VCH.
```
./vic-machine-darwin configure \
--target lab-vcsa67-001.lab.jarvis.local/Datacenter-North \
--user adm.jarvis@lab.jarvis.local \
--thumbprint 4F:D3:9B:50:00:31:D9:84:9D:DA:CF:57:21:D6:0D:11:89:78:97:26 \
--id vm-212 \
--container-network vic-tam-container:container-net \
--container-network-gateway vic-tam-container:192.168.100.1/24 \
--container-network-ip-range vic-tam-container:192.168.100.0/24 \
--container-network-dns vic-tam-container:192.168.100.80
```

### Add path for registry certificates

> NOTE: By default docker only allows to run images from trusted registries. If you are using self-signed certs on VIC, use the following command to configure your VCH.

```
./vic-machine-linux configure\
--target=https://10.40.206.195\
--thumbprint=A7:23:5A:12:BB:BF:92:9A:12:62:71:53:60:12:EF:2E:AA:EC:59:FD\
--name=vch1\
--compute-resource=/lab/host/VIC/Resources\
--registry-ca /etc/docker/certs.d/registry.corp.local/ca.crt
```

For adding other insecure registries, use the following command line option to the above command:

```
--insecure-registry=registry.corp.local \
```

Whitelisting Registries:

```
--whitelist-registry vic01.lab.jarvis.local \
--whitelist-registry registry.hub.docker.com \
```

### Reset a hanging progress.
```
./vic-machine-darwin configure \
--target lab-vcsa67-001.lab.jarvis.local/Datacenter-North \
--user adm.jarvis@lab.jarvis.local \
--thumbprint 4F:D3:9B:50:00:31:D9:84:9D:DA:CF:57:21:D6:0D:11:89:78:97:26 \
--id vm-1010 \
--reset-progress
```

### This will create a VM/Host Group which will automatically add the VCH as well as all running cVM´s into it.
```
./vic-machine-darwin configure \
--target lab-vcsa67-001.lab.jarvis.local/Datacenter-South \
--user administrator@jarvis.local \
--thumbprint 4F:D3:9B:50:00:31:D9:84:9D:DA:CF:57:21:D6:0D:11:89:78:97:26 \
--id vm-1375 \
--volume-store vsanDatastore/volumes:default 
--affinity-vm-group
```