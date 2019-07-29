# tutorial-k8s-dashbord
Tutorial on creating a K8S dashboard using a cluster created with my other personal project vagrant-kube

## Status

For now I just added the config files to use. I will write later on how to use them, and why I edited them in that way

## Steps

- Create a cluster using the project vagrant-kube. I used 2 workers + a master with standard config and the 192.168.195.0/24 subnet. See the README on that project to do that. You'll need vagrant and virtualbox.
- SSH into the master, and copy the kubeconfig file into /vagrant (the shared folder)
- Suppose your kubeconfig file is in /path/kubeconfig. You can access that context simply by:  
export KUBECONFIG=/path/kubeconfig:$HOME/.kube/config:$KUBECONFIG
- Now your kubectl get contexts should have a new context to use. TODO Use kubeadm better in vagrant-kube to better metadata
- Use the kubernetes-dashboard.yaml deployment. Change IP addresses in service configuratiion section if necessary.
- Create the role for dashboard to access the cluester data with the token. Use kubectl get secret -n kube-system, and then: kubectl describe secrets dashboard-do-token-smlqx -n kube-system...
- You can fix a logging issue with the dashboard about using heapster: https://github.com/rancher/rancher/issues/15784
