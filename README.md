# My Deployment

Where I deploy software

## Start ArgoCD

Navigate into dev overlays and uncomment secret to apply GCP `credenditals.json` secret.

```sh
cd distribution/argocd/overlays/dev/kustomization
```

```yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
namespace: argocd

resources:
  ## Common
- ../../base/
## Only on initial deployment of argocd
# - env/secret-gcp-kms.yaml
```

Build and apply with `kustomize`

```sh
kustomize build distribution/argocd/overlays/dev | kubectl apply -f -
```

## Create encrypted secret

```sh
gcloud kms keys list --location global --keyring sops

KEY_LOCATION='project/<project_id>/locations/global/keyRings/<name>/<type>/<key>

sops --encrypt --gcp-kms $KEY_LOCATION secret.yaml > secret.enc.yaml
```
