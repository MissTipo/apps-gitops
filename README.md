# apps-gitops

GitOps repository for deploying application workloads to the platform.  
ArgoCD continuously reconciles the environment from this repository.

This repo contains:

- Application Helm charts
- Kustomize base + overlays (dev, staging, prod)
- ArgoCD Application and ApplicationSet definitions
- Progressive delivery configs (Argo Rollouts)
- GitOps-driven image promotion workflows

---

## Structure

```
apps-gitops/
  services/
    user-api/
      helm-chart/
      kustomize/
        base/
        overlays/
          dev/
          staging/
          prod/
      argo-application.yaml
    worker/
      helm-chart/
      kustomize/
        base/
        overlays/
          dev/
          staging/
          prod/
      argo-application.yaml
    frontend/
      helm-chart/
      kustomize/
        base/
        overlays/
          dev/
          staging/
          prod/
      argo-application.yaml
  rollouts/
    user-api/
  ci/
    image-promotion.yml
```

---

## GitOps Workflow

1. CI builds & pushes an image.
2. CI updates the `dev` overlay with the new tag.
3. ArgoCD deploys to `dev`.
4. Promotion to `staging` and `prod` occurs through PRs.

---

## Purpose

This repo aligns with:
- CAPA (ArgoCD, RBAC, AppProjects, sync hooks, Rollouts)
- CKA (workload admin, troubleshooting, deployment strategies)

