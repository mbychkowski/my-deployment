# My Deployment

Where I deploy software

## Start ArgoCD

```sh
kustomize build distribution/argocd/base/ | kubectl apply -f -
```
