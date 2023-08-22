# fmt2-argocd
This repo stores all the Argo configuration files for our FMT2 Kubernetes cluster.

## Accessing ArgoCD
https://10.3.4.1 is the LoadBalancer IP for Argo.

TODO: Make this a Traefik endpoint
TODO: Add real authenication too.

## Adding a namespace
Namespaces should be added in apps/infra/namespaces in order to keep track of all the namespaces that is sprayed in our cluster.