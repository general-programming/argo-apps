# fmt2-argocd
This repo stores all the Argo configuration files for our FMT2 Kubernetes cluster.

## Deploying ArgoCD
```
kubectl create namespace argocd
kubectl apply -k argocd/<datacenter>

# start port forward
kubectl port-forward svc/argocd-server -n argocd 8080:443

# add ssh key and add root
nix shell nixpkgs#argocd
argocd login localhost:8080 --username admin --password $(kubectl -n argocd get -o json secret argocd-initial-admin-secret | jq .data.password -r | base64 -d)
argocd repo add git@github.com:general-programming/argo-apps.git --ssh-private-key-path fmt2-argo
argocd cluster set in-cluster --name <datacenter>
kubectl apply -f bootstrap.yaml
```

## get temp pass
```
kubectl -n argocd get -o json secret argocd-initial-admin-secret | jq .data.password -r | base64 -d
```

## Accessing ArgoCD
https://10.3.4.1 is the LoadBalancer IP for Argo.

TODO: Make this a Traefik endpoint
TODO: Add real authenication too.

## Adding a namespace
Namespaces should be added in apps/infra/namespaces in order to keep track of all the namespaces that is sprayed in our cluster.