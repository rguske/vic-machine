## `vic-machine inspect`

Will `inspect` an existing (already deployed) Virtual Container Host and shows important data like e.g. the **Docker environment variables** or the **Docker endpoint data**.

> *Please adjust the environment parameters accordingly to yours!*

```
./vic-machine-linux inspect \
--name mk5 \
--target vcsa.jarvis.lab/Stark-Industries \
--user jarvis@jarvis.lab \
--thumbprint 55:AC:B3:2D:9B:56:62:F4:1B:C2:EC:78:......
```

Example output:

```
./vic-machine-linux inspect \
--name mk5 \
--target vcsa.jarvis.lab/Stark-Industries \
--user vic@jarvis.lab \
--thumbprint 55:AC:B3:2D:9B:56:62:F4:1B:C2:EC:78:71:36:B9:DD:A5:20:D7:FD
INFO[0000] vSphere password for vic@jarvis.lab:      
INFO[0003] ### Inspecting VCH ####                      
INFO[0003] Validating target                            
INFO[0004]                                              
INFO[0004] Installer version: v1.5.5-21324-50a44954     
INFO[0004] VCH version: v1.5.5-21324-50a44954           
INFO[0004]                                              
INFO[0004] VCH upgrade status:                          
INFO[0004] Installer has same version as VCH            
INFO[0004] No upgrade available with this installer version 
INFO[0004] Using address mk5.jarvis.lab from host certificate for host address over assigned client IP 10.10.13.5 
INFO[0004] --tls-cert-path not supplied - checking for certs in current directory, mk5/ and /home/rguske/.docker/ 
INFO[0004]                                              
INFO[0004] VCH ID: vm-14989                             
INFO[0004]                                              
INFO[0004] VCH Admin Portal:                            
INFO[0004] https://mk5.jarvis.lab:2378                  
INFO[0004]                                              
INFO[0004] VCH Default Bridge Network Range: 10.10.0.0/16 
INFO[0004] VCH Default Bridge Network Width: 16         
INFO[0004]                                              
INFO[0004] Published ports can be reached at:           
INFO[0004] 10.10.13.5                                   
INFO[0004]                                              
INFO[0004] Management traffic will use:                 
INFO[0004] 10.10.13.5                                   
INFO[0004]                                              
INFO[0004] Docker environment variables:                
INFO[0004] DOCKER_TLS_VERIFY=1 DOCKER_CERT_PATH=/home/rguske/Downloads/vic/mk5 DOCKER_HOST=mk5.jarvis.lab:2376 COMPOSE_TLS_VERSION=TLSv1_2 
INFO[0004]                                              
INFO[0004] Connect to docker:                           
INFO[0004] docker -H mk5.jarvis.lab:2376 --tlsverify info 
INFO[0004] Completed successfully
```