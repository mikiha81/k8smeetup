 ** RANCHER
   install : 
   docker run -d --restart=unless-stopped \
  -p 80:80 -p 443:443 \
  --privileged \
  rancher/rancher:latest



** kubespray 

   https://kubernetes.io/docs/setup/production-environment/tools/kubespray/



**  install kubeadmin 


 sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl 
sudo curl -fsSLo /usr/share/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/usr/share/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl

sudo kubeadm init --pod-network-cidr=192.168.0.0/16

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl create -f https://docs.projectcalico.org/manifests/tigera-operator.yaml
kubectl create -f https://docs.projectcalico.org/manifests/custom-resources.yaml
kubectl taint nodes --all node-role.kubernetes.io/master-
kubectl get nodes -o wide



** prometheus operator

https://operatorhub.io/operator/prometheus



curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.18.2/install.sh | bash -s v0.18.2
kubectl create -f https://operatorhub.io/install/prometheus.yaml
kubectl get csv -n operators


---------------------
git clone https://github.com/coreos/prometheus-operator.git
git clone https://github.com/mateobur/prometheus-monitoring-guide.git


kubectl create -f prometheus-operator/contrib/kube-prometheus/manifests/
