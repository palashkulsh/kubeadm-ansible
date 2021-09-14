  * docker role is not good, use nickjj docker_setup.yaml
  * private ip subnet all via firewall-cmd 
  `sudo firewall-cmd --zone=trusted --add-source=172.16.0.0/20 --permanent`
  `sudo firewall-cmd --reload`

  * remove /etc/containerd/config.toml from master node as it has some systemd conflicts
  
  * container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:docker: network plugin is not ready: cni config uninitialized
  `curl https://docs.projectcalico.org/manifests/calico.yaml -O
  kubectl apply -f calico.yaml`

  * `kubectl get cs` gives unhealthy scheduler, to solve it https://stackoverflow.com/questions/54608441/kubectl-connectivity-issue

  * if adding apt repo of kubernetes fails https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/
    * was getting apt cache update failed for 1 worker node
    
  * for debugging kubernetes https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/
  * https://www.engineerbetter.com/blog/debugging-kubernetes-networking/


    ```
  ubuntu@launched-from-terraform-16970:/etc$ route -n
  Kernel IP routing table
  Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
  0.0.0.0         172.16.0.1      0.0.0.0         UG    100    0        0 enp0s3
  10.244.109.192  172.16.0.92     255.255.255.192 UG    0      0        0 tunl0
  10.244.161.0    172.16.0.201    255.255.255.192 UG    0      0        0 tunl0
  10.244.235.128  0.0.0.0         255.255.255.192 U     0      0        0 *
  10.244.235.129  0.0.0.0         255.255.255.255 UH    0      0        0 calib46d9bed3f5
  10.244.235.133  0.0.0.0         255.255.255.255 UH    0      0        0 calif81e7fd5ae6
  10.244.244.128  172.16.0.37     255.255.255.192 UG    0      0        0 tunl0
  169.254.0.0     0.0.0.0         255.255.0.0     U     100    0        0 enp0s3
  172.16.0.0      0.0.0.0         255.255.255.0   U     0      0        0 enp0s3
  172.17.0.0      0.0.0.0         255.255.0.0     U     0      0        0 docker0
  ```

  * for rule based output `sudo iptables-save`
  * for tabular output `sudo iptables -L -v -n `


### how to install calicoctl 

  * to install calicoctl https://docs.projectcalico.org/getting-started/clis/calicoctl/install
    * curl -o kubectl-calico -O -L  "https://github.com/projectcalico/calicoctl/releases/download/v3.19.2/calicoctl-linux-arm64"
  * to troubleshoot calico https://docs.projectcalico.org/maintenance/troubleshoot/troubleshooting


### allow all protocols in terraform for 172.16 and 10.0 subnets
### debian uses nftables for iptables, so update to iptables legacy https://stackoverflow.com/questions/61978030/kubernetes-pods-not-accessible-within-the-cluster

### allow kube-proxy to read kube root certificate
`kubectl edit role kube-proxy -n kube-system`


  * find ip routes from ip 1 to ip 2
    * `ip route get to ip1 from ip2`
    * `ip route show` or `route -n`
