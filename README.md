# Retail Data Platform — GitOps Repository

This repository is the **source of truth for Kubernetes manifests** for the Retail Data Platform. It is watched by ArgoCD running in the dev GKE cluster.

## Structure

- `apps/` — one subfolder per application, containing its Kubernetes manifests
- `argocd/` — ArgoCD `Application` resources that register each app folder with the cluster

## How It Works

1. You commit a change to a manifest under `apps/`.
2. ArgoCD polls this repo every 3 minutes.
3. ArgoCD applies the change to the cluster.
4. The cluster converges to match the repo.

Git is the desired state. The cluster reflects it.