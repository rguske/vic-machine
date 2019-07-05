## `vic-machine create` will, like the name is promising you, create a Virtual Container Host for you, which will provide the Docker-Endpoint for your Developers.

> A VCH is the virtual functional equivalent of a Linux VM running Docker. From a Docker client point of view, the Virtual Container Host looks very similar to a native Docker host. Hence, there are differences between a native Docker host and a Virtual Container Host (VCH), and between a Linux container and a container VM.

**Source:** <a href="https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/vsphere/vmware-vsphere-integrated-containers-white-paper.pdf" target="_blank">Architecture Overview (VIC 1.2)</a>

See: <a href="https://rguske.github.io/post/vsphere-integrated-containers-part-iii-deployment-of-a-virtual-container-host/" target="_blank">vSphere Integrated Containers Part III: Deployment of a Virtual Container Host</a>

> *Please beare in mind that the following example(s) are all based on my homelab parameters*

### VCH deployment with the option tls-cname. *Static DNS entry was made manually before (workaround)*.

```
./vic-machine-darwin create \                             ### vic-machine binary + action
--name vch-example \                                      ### Name of the Virtual Conatiner Host
--syslog-address udp://10.10.10.10:514 \                  ### Syslog server
--target vcenter.example.org/Datacenter \                 ### vSphere Datacenter
--user administrator@vsphere.local \                      ### User with appropriate privileges
--compute-resource /Datacenter/host/Cluster \             ### vSphere Cluster or single ESXi Host
--image-store vsanDatastore \                             ### Datastore to deposite the images
--volume-store vsanDatastore/volumes:default \            ### Datastore for the Docker Volumes (VMDKs)
--bridge-network ls-vic-bridge \                          ### vDS dPort Group for the Container Bridge Network
--bridge-network-range 172.16.0.0/12 \                    ### Network range for the Bridge Network
--public-network ls-vic-public \                          ### vDS dPort Group for the Public Network
--dns-server 10.10.10.254 \                               ### DNS Server address for the Public Network
--public-network-ip=10.10.10.11/24 \                      ### Static IP address for the Virtual Container Host
--public-network-gateway 10.10.10.254 \                   ### Gateway for the Public network
--tls-cname=vch-example.example.org \                     ### Certificate Common Name (CN) for the VCH
--certificate-key-size 3072 \                             ### Key size for the auto-generated certificates
--organization example.org \                              ### Certificate Organization (O) field
--registry-ca=/folder path/ca.crt \                       ### Path to the VIC (Harbor) ca.crt file
--thumbprint 4C:92:D7:FC:F8:8D:5A:9F:.... \               ### vCenter Server Thumbprint
--affinity-vm-group \                                     ### Automatically creates a VM/Host Group (cVM/ VCH Group)
--ops-user vic-devops-admin@example.org \                 ### Defines the user which is used by the VCH to interact with vSphere
--ops-grant-perms                                         ### Automatically grants the necessary vSphere permissions
```

### VCH deployment with a dedicated Network for the Container-VMs and additional options.

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
--dns-server 10.10.10..254 \
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
