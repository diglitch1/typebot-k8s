# Quickstart 
> note: will finish the todos after thursday :thumbsup:

run this to create the cluster: 

TODO: add explaination to this part `8082:80@loadbalancer`
```bash
k3d cluster create -p 8082:80@loadbalancer
```
add this into your `/etc/hosts`:
```bash
127.0.0.1 builder.typebot.local viewer.typebot.local
```
The ingress uses these hostnames.


run this and then change `forward . /etc/resolv.conf` to `forward . 1.1.1.1 8.8.8.8` TODO: add explaination on why you need to change this

```bash
kubectl -n kube-system edit configmap coredns
```

after that run this to apply the changes:  TODO: explain why & what it does 
```bash
kubectl -n kube-system rollout restart deployment/coredns
```

now first apply the cnpg helmfile: 
```bash
helmfile -f cnpg-helmfile.yaml apply
```

to check whether you are ready to apply the typebot helmfile make sure to check this stuff:

```bash
kubectl get pods -n cnpg-system
kubectl get endpoints -n cnpg-system cnpg-webhook-service
```

once everything is `running` or `completed` apply the typebot-helmfile: 
```bash
helmfile -f typebot-helmfile.yaml apply
```
this can take up to 10-15 minutes so watch to see once its done: 
```bash
kubectl get pods -w 
```
check: 

```bash
kubectl get pvc 
kubectl get cluster 
kubectl get secrets 
kubectl get pods 
```

now go to http://builder.typebot.local:8082 and sign in :thumbsup:

