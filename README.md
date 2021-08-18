# My Deployment

Where I deploy software

## Start ArgoCD

```sh
kustomize build distribution/argocd/overlays/dev | kubectl apply -f -
```

## Create encrypted secret

```sh
gcloud kms keys list --location global --keyring sops

KEY_LOCATION='project/<project_id>/locations/global/keyRings/<name>/<type>/<key>

sops --encrypt --gcp-kms $KEY_LOCATION secret.yaml > secret.enc2.yaml
```
