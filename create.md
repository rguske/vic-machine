## `vic-machine create`

By using `vic-machine create` a Virtual Container Host (VCH) will be deployed to your vSphere Environment. The VCH will provide the Docker-Endpoint for your Developers.

> A VCH is the virtual functional equivalent of a Linux VM running Docker. From a Docker client point of view, the Virtual Container Host looks very similar to a native Docker host. Hence, there are differences between a native Docker host and a Virtual Container Host (VCH), and between a Linux container and a container VM.

**Source:** [Architecture Overview (VIC 1.2)](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/vsphere/vmware-vsphere-integrated-containers-white-paper.pdf)

See: [vSphere Integrated Containers Part III: Deployment of a Virtual Container Host](https://rguske.github.io/post/vsphere-integrated-containers-part-iii-deployment-of-a-virtual-container-host/)

> *Please adjust the environment parameters accordingly to yours!*

### VCH deployment with the just mandatory network configuration (public and bridge)*.

```
./vic-machine-darwin create \
--name vch-example \
--syslog-address udp://10.10.10.10:514 \
--target vcenter.example.org/Datacenter \
--user administrator@vsphere.local \
--compute-resource /Datacenter/host/Cluster \
--image-store vsanDatastore \
--volume-store vsanDatastore/volumes:default \
--bridge-network ls-vic-bridge \
--bridge-network-range 172.16.0.0/12 \
--public-network ls-vic-public \
--dns-server 10.10.10.254 \
--public-network-ip=10.10.10.11/24 \
--public-network-gateway 10.10.10.254 \
--tls-cname=vch-example.example.org \
--certificate-key-size 3072 \
--organization example.org \
--registry-ca=/folder path/ca.crt \
--thumbprint 4C:92:D7:FC:F8:8D:5A:9F:.... \
--affinity-vm-group \
--ops-user vic-devops-admin@example.org \
--ops-grant-perms
```

### VCH deployment with a dedicated Network for the Container-VMs and more advanced options like e.g. resource configuration options for the VCH.

```
./vic-machine-darwin create \
--name vch-example02 \
--container-name-convention mark_{name} \
--syslog-address udp://10.10.10.10:514 \
--target vcenter.example.org/Datacenter \
--compute-resource /Datacenter/host/Cluster \
--cpu-reservation 1 \
--cpu-shares normal \
--memory-reservation 1 \
--memory-shares normal \
--endpoint-cpu 1 \
--image-store vsanDatastore/default \
--base-image-size 8GB \
--bridge-network vic-bridge \
--bridge-network-range 172.16.0.0/12 \
--public-network vic-public \
--dns-server 10.10.10.254 \
--container-network vic-container:container-net \
--container-network-gateway vic-container:192.168.100.1/24 \
--container-network-ip-range vic-container:192.168.100.0/24 \
--container-network-dns vic-container:192.168.100.80 \
--tls-cname vch-example02 \
--organization example.org \
--certificate-key-size 3072 \
--no-tlsverify \
--user administrator@vsphere.local \
--thumbprint 4F:D3:9B:50:00:31:D9:... \
--ops-user vic-devops-admin@example.org \
--ops-grant-perms
```
