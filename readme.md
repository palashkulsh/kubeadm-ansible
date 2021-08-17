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
