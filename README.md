# k8sNotes
# install
---------
##### init with flannel
```bash
        kubeadm init --pod-network-cidr=10.244.0.0/16
```

##### gain kubectl power
```bash
        cp /etc/kubernetes/admin.conf || kubelet.conf $HOME/
        chown $(id -u):$(id -g) $HOME/admin.conf || kubelet.conf
        export KUBECONFIG=$HOME/admin.conf || kubelet.conf
```

##### reset iptable
```bash
        iptables -F && iptables -t nat -F && iptables -t mangle -F && iptables -X
```

##### dashboard
```
       https://medium.com/@sondnpt00343/deploying-a-publicly-accessible-kubernetes-dashboard-v2-0-0-betax-8e39680d4067
```

kubeadm join 192.168.1.11:6443 --token 3yy5l2.lxfmc3vi7l1888a4 \
    --discovery-token-ca-cert-hash sha256:c58fe1a941c05dee5bb7344c696e6baee82b8d320c33bcd5b89a86143a2b258a 


##### nginx-ingress
   external-ip pandding:
```
   edit svc
             externalIPs:
               - xx.xx.xx.xx
```
   open ssl
```
   edit deployment
       spec:
         containers:
         - args:
            - /nginx-ingress-controller
            - --enable-ssl-passthrough  # this line
 ```
 ##### dashboard
 ```
 # as /dashboard
 ingress
      annotations:
        nginx.ingress.kubernetes.io/ingress.class: "nginx"
        nginx.ingress.kubernetes.io/backend-protocol: "HTTPS"
        nginx.ingress.kubernetes.io/rewrite-target: /$2'
        nginx.ingress.kubernetes.io/configuration-snippet: rewrite ^(/dashboard)$ $1/ redirect;
      paths:
        - path: /dashboard(/|$)(.*)
```

```
#  token expiretime : deployment
       args:
        - --token-ttl=0
```
##### longhorn
```
# longhorn in subpath use image:
   wangsiye/longhorn-ui:d99673b
```
