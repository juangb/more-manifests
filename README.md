Related to: https://github.com/argoproj/applicationset/issues/593

# Description
Test applicationset-controller refresh time.

## KIND
kind create cluster --image kindest/node:v1.24.7@sha256:577c630ce8e509131eab1aea12c022190978dd2f745aac5eb1fe65c0807eb315
kubectl config use-context kind-kind

## Install ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f install.yaml
kubectl apply -f cm-configmap.yml -n argocd
kubectl apply -f rbac-configmap.yml -n argocd

# Install ApplicationSet
kubectl apply -f apps/builder-tools-applicationset-services.yml

# Load image to kind nodes
kind load docker-image argocd:fix-appset-v2