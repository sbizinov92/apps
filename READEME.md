# 🚀 ArgoCD Bootstrap Applications

This repository defines a set of ArgoCD `Application` manifests used to bootstrap essential infrastructure components into a Kubernetes cluster.

# NOTE

> Repos now also created manually via ArgoCD UI argocd github app configured for this repo.

> During the initial bootstrap, a small amount of manual setup ("click ops") was used to configure ArgoCD access and to apply these application manifests. This was intentional to avoid circular dependencies during the very first deployment (e.g., cert-manager, ingress, ArgoCD itself).

---

## 📦 Applications

The following components are managed by ArgoCD and will be automatically deployed and kept in sync:

### 1. **cert-manager**
- **Source:** [`sbizinov92/apps`](https://github.com/sbizinov92/apps) – `cert-manager/`
- **Destination:** `cert-manager` namespace
- **Features:** Auto-sync, pruning, self-healing, namespace creation

### 2. **AWS Load Balancer Controller**
- **Source:** [`sbizinov92/apps`](https://github.com/sbizinov92/apps) – `aws-load-balancer-controller/`
- **Destination:** `kube-system` namespace
- **Features:** Auto-sync, pruning, self-healing

### 3. **echo-server**
- **Source:** [`sbizinov92/echoserver`](https://github.com/sbizinov92/echoserver) – Helm chart at `charts/echoserver/`
- **Destination:** `echoserver` namespace
- **Features:** Auto-sync, pruning, self-healing, namespace creation

---

## 📁 Structure

Each file here (`*.yml`) represents an ArgoCD `Application` custom resource that can be applied using:

```bash
kubectl apply -f <file>.yml -n argocd