# ops-infrastructure

This repository contains the necessary files to set up Flux for GitOps on a Kubernetes cluster.

## GCP Authentication

Authenticate to Google Cloud.

```bash

gcloud auth login --update-adc &&
export GOOGLE_OAUTH_ACCESS_TOKEN=$(gcloud auth print-access-token) &&
export PROJECT_ID=$(gcloud config get-value project)

```

## Clusters

### rubix-control1

Files and Their Purposes

1. `clusters/rubix-control1/helmrelease.yaml`: Defines the Helm release for ArgoCD, specifying the chart details and custom values.

2. `clusters/rubix-control1/helmrepository.yaml`: Specifies the Helm repository for ArgoCD.

3. `clusters/rubix-control1/kustomization.yaml`: Ties together the Helm release and repository resources.


## Bootstrap flux

Run bootstrap for a private repository hosted on GitHub Enterprise using SSH auth
  `flux bootstrap github --owner=<organization> --repository=<repository name> --hostname=<domain> --ssh-hostname=<domain> --path=clusters/my-cluster`

```bash

➜ ssh-keygen -q -N "" -f ./identity

## Devbox Instructions

1. Install [Devbox](https://www.jetify.com/devbox) if it is not already installed.

1. `Devbox shell` this will install the Flux CLI

## Reference

### ArgoCD

```bash 


helm install argocd argo/argo-cd \
 --namespace argocd \
 --create-namespace \
 --set global.image.repository=docker-upstream.apple.com/argoproj/argocd \
 --set global.image.tag=v2.13.3 \
 --set global.image.imagePullPolicy=IfNotPresent

 ```
