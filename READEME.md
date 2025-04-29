# 🚀 ArgoCD Bootstrap Applications

This repository defines a set of ArgoCD `Application` manifests used to bootstrap essential infrastructure components into a Kubernetes cluster.

## ⚠️ Notes

> - Some repositories (such as `apps`) were manually added via the ArgoCD UI. The GitHub App integration is configured for this repository.
> - During the initial bootstrap, a small amount of manual setup ("click ops") was used to configure ArgoCD access and apply these application manifests. This was intentional to avoid circular dependencies during the first deployment (e.g., cert-manager, ingress, ArgoCD itself).
> - **Note:** The `cert-manager` and `aws-load-balancer-controller` applications currently do not include node selectors or tolerations. As a result, their pods may be scheduled on unintended nodes if you are using node pools with taints and roles (e.g., system vs. application separation).


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