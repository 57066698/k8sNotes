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
       
       kubectl -n kube0system edit deployments kubernetes-dashboard
       --token-ttl=0
```


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
##### change default storage class
```
kubectl get storageclass
kubectl patch storageclass gold -p '{"metadata": {"annotations":{"storageclass.kubernetes.io/is-default-class":"true"}}}'
```
