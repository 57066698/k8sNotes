# k8sNotes
### k8s install
```python
        # init with flannel
        kubeadm init --pod-network-cidr=10.244.0.0/16
        # gain kubectl power
        cp /etc/kubernetes/admin.conf || kubelet.conf $HOME/
        chown $(id -u):$(id -g) $HOME/admin.conf || kubelet.conf
        export KUBECONFIG=$HOME/admin.conf || kubelet.conf
        # reset iptable
        iptables -F && iptables -t nat -F && iptables -t mangle -F && iptables -X
```

kubeadm join 192.168.1.11:6443 --token 3yy5l2.lxfmc3vi7l1888a4 \
    --discovery-token-ca-cert-hash sha256:c58fe1a941c05dee5bb7344c696e6baee82b8d320c33bcd5b89a86143a2b258a 
