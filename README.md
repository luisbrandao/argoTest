# ArgoCD Example Application

This repository contains a simple application scaffold for ArgoCD deployment demonstration.

## Structure

- `k8s/` - Kubernetes manifests
  - `namespace.yaml` - Namespace definition
  - `deployment.yaml` - Application deployment
  - `service.yaml` - Service definition

## ArgoCD Application

To deploy this with ArgoCD, create an Application resource pointing to this repository:

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: example-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: <YOUR_REPO_URL>
    targetRevision: HEAD
    path: k8s
  destination:
    server: https://kubernetes.default.svc
    namespace: example-app
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
    - CreateNamespace=true
```

## Deployment

ArgoCD will automatically sync and deploy the application when connected to this repository.
