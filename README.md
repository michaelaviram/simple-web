# Helm Chart Jenkins Pipeline

## Overview

This repository contains a Helm Chart and Jenkinsfile for installing and uninstalling the chart on a dedicated AKS cluster. The Helm Chart deploys a request-counting app.

## Running the Pipeline

Log into the Jenkins server at http://4.180.159.141:8080 with the provided credentials, choose "helm_chart" project and click "Build with Parameters". Select either "Deploy" or "Destroy" and click "Build".

* "Deploy" will install the Helm Chart on the AKS Cluster.
* "Destroy" will uninstall it.

To confirm deployment, visit: http://98.64.41.189/michael

## The Helm Chart

The helm chart is comprised of a values.yaml and four manifest templates:
- Deployment
- Service
- Ingress
- Auto-scaler - A KEDA scaledObject costume resource

### Autoscaler Triggers
- CPU
- Memory
- Peak Hours Cron job
- Off Peak Cron job

## The Pipeline

### Stages:

1. Clean - Cleans the Jenkins workspace.
2. Checkout - Clones the files from this repository.
3. Connect to Cluster - Connects to the AKS cluster via az CLI and kubelogin.
4. Chart Deploy - Deploys the Chart with Helm Install. Skipped if the parameter "Destroy" is selected.
5. Chart Destroy - Uninstall the Release with Helm Uninstall. Skipped if the parameter "Deploy" is selected.

### Idempotence
To keep the pipeline idempotent, the "Connect to Cluster", "Chart Deploy" and "Chart Destroy" stages include checks to skip them in case of prior configuration.








