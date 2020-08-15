# k8sNotes
### k8s install
```python
        # init with flannel
        kubeadm init --pod-network-cidr=10.244.0.0/16
        
        # reset iptable
        iptables -F && iptables -t nat -F && iptables -t mangle -F && iptables -X
```
