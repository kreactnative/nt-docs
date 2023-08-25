#### unlock version
```
yum versionlock clear
```
#### check version 
```
yum list --showduplicates kubeadm --disableexcludes=kubernetes
```
#### Upgrading master node 01
```
yum install -y kubeadm-1.27.3-0 --disableexcludes=kubernetes
kubeadm version
kubeadm upgrade plan
sudo kubeadm upgrade apply v1.27.3
yum install -y kubelet-1.27.3-0 kubectl-1.27.3-0 --disableexcludes=kubernetes
sudo dnf versionlock kubelet kubeadm kubectl
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```
#### Upgrading master node other
```
yum install -y kubeadm-1.27.3-0 --disableexcludes=kubernetes
kubeadm version
kubeadm upgrade plan
sudo kubeadm upgrade node
yum install -y kubelet-1.27.3-0 kubectl-1.27.3-0 --disableexcludes=kubernetes
sudo dnf versionlock kubelet kubeadm kubectl
sudo systemctl daemon-reload
sudo systemctl restart kubelet
```
#### upgrade worker node
```
yum install -y kubeadm-1.27.3-0 --disableexcludes=kubernetes
sudo kubeadm upgrade node
yum install -y kubelet-1.27.3-0 kubectl-1.27.3-0 --disableexcludes=kubernetes
sudo dnf versionlock kubelet kubeadm kubectl
sudo systemctl daemon-reload
sudo systemctl restart kubelet

```