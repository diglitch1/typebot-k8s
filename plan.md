# to-do
- [x] cnpg (postgres)
- [x] redis
    - implement pvc (even though redis in this case is only being used for cache)
    - (redis sentinel?)
- [ ] ingress
- [ ] helm chart
- [ ] namespaces

# notes
no more minikube → slow as f**k (because it is made for k8s which has alot of bloat like objects for rnd cloud providors, which are not needed here)
therefor switched to k3s!

```bash
# to fetch DATABASE_URL
kubectl apply --server-side -f \
  https://raw.githubusercontent.com/cloudnative-pg/cloudnative-pg/release-1.29/releases/cnpg-1.29.1.yaml
```

```bash
# add /etc/hosts 
127.0.0.1        builder.typebot.local viewer.typebot.local
```

```bash
# purge secrets from git history
git filter-repo --path typebot-secret.yaml --invert-paths --force
```
```bash
kc port-forward typebot-builder-deployment-5955bc65ff-5v29r 8083:3000
```

[http://builder.typebot.local:8082/signin](http://builder.typebot.local:8082/signin)