# Simple-Web Helm Assignment

## Overview

This repository contains a Helm Chart and Jenkinsfile for installing and uninstalling the chart on a dedicated AKS cluster.

## The Helm Chart

The helm chart is comprised of a values.yaml and four manifest templates:
- Deployment
- Service
- Ingress
- ScaledObject

## The Pipeline

The pipeline triggers manually from the Jenkins server. The pipeline is parameterised, and requires manual selection of either to Deploy or Destroy the chart on the Cluster.

### It includes five stages:
1. Clean - Cleans the Jenkins workspace.
2. Fetch - Clones the files from this repository.
3. Connect to Cluster - Connects to the AKS cluster via az CLI and kubelogin.
4. Chart Deploy - Deploys the Chart with Helm Install. Skipped if the parameter "Destroy" is selected.
5. Chart Destroy - Uninstall the Release with Helm Uninstall. Skipped if the parameter "Deploy" is selected.

### Idempotence
To keep the pipeline idempotent, the "Connect to Cluster", "Chart Deploy" and "Chart Destroy" stages include checks to skip them in case of prior configuration.

### Environment Variables






