---
description: 'HG: Can skip this entire "deployment guide" section.'
---

# Deployment Guide

The document is intended for an audience with a stable technical knowledge that would like to setup an environment for development, testing and contributing to the Mojaloop project.

## Deployment and Setup

* [Pre-requisites](./#1-pre-requisites)
* [Kubernetes](./#3-kubernetes)
  * [Kubernetes Dashboard](./#31-kubernetes-dashboard)
* [Helm](./#4-helm)
  * [Helm configuration](./#41-helm-configuration)
* [Postman](./#6-postman)
  * [Installing Postman](./#61-installing-postman)
  * [Setup Postman](./#62-setup-postman)

### 1. Pre-requisites

Versions numbers below are hard requirements, not just recommendations \(more recent versions are known not to work\).

A list of the pre-requisite tool set required for the deployment of Mojaloop:

* **Kubernetes** An open-source system for automating deployment, scaling, and management of containerized applications. Find out more about [Kubernetes](https://kubernetes.io),

   
  _Recommended Versions:_

   
      _**Mojaloop Helm Chart release v11.x** supports **Kuberentes v1.13 - v1.17**, newer versions have not been tested._

   
      _**Mojaloop Helm Chart release v10.x** supports **Kuberentes v1.13 - v1.15**, it will fail on Kuberentes v1.16+ onwards due deprecated APIs \(_[_ref: Helm Issue \#219_](https://github.com/mojaloop/helm/issues/219)_\)._

  * kubectl - Kubernetes CLI for Kubernetes Management is required. Find out more about [kubectl](https://kubernetes.io/docs/reference/kubectl/overview/):
    * [Install-kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/),
  * microk8s - MicroK8s installs a barebones upstream Kubernetes for a single node deployment generally used for local development. We recommend this installation on Linux \(ubuntu\) OS. Find out more about [microk8s](https://microk8s.io/) and [microk8s documents](https://microk8s.io/docs/):
    * [Install-microk8s](https://microk8s.io/docs/),
  * kubectx - Not required but useful. Find out more about [kubectx](https://github.com/ahmetb/kubectx),
  * kubetail - Not required but useful. Bash script that enables you to aggregate \(tail/follow\) logs from multiple pods into one stream. Find out more about [kubetail](https://github.com/johanhaleby/kubetail),

* **Docker** Provides containerized environment to host the application. Find out more about [Docker](https://docker.com),
* **Helm** A package manager for Kubernetes. Find out more about [Helm](https://helm.sh),

   
  _Recommended Versions:_

   
      _**Helm v3.x** \(_[_ref: Design Auth Issue \#52_](https://github.com/mojaloop/design-authority/issues/52)_\)._

* **Postman** Postman is a Google Chrome application for the interacting with HTTP API's. It presents you with a friendly GUI for the construction requests and reading responces.    [https://www.getpostman.com/apps](https://www.getpostman.com/apps). Find out more about [Postman](https://postman.com).

For **local guides** on how to setup the pre-requisites on your laptop or desktop, refer to the appropriate link document below;

* [Local Setup for Mac](local-setup-mac.md)
* [Local Setup for Linux](local-setup-linux.md)
* [Local Setup for Windows](local-setup-windows.md)

### 2. Deployment Recommendations

This provides environment resource recommendations with a view of the infrastructure architecture.

**Resources Requirements:**

* Control Plane \(i.e. Master Node\)

  [https://kubernetes.io/docs/setup/cluster-large/\#size-of-master-and-master-components](https://kubernetes.io/docs/setup/cluster-large/#size-of-master-and-master-components)

  * 3x Master Nodes for future node scaling and HA \(High Availability\)

* ETCd Plane:

  [https://etcd.io/docs/v3.3.12/op-guide/hardware](https://etcd.io/docs/v3.3.12/op-guide/hardware)

  * 3x ETCd nodes for HA \(High Availability\)

* Compute Plane \(i.e. Worker Node\):

  TBC once load testing has been concluded. However the current general recommended size:

  * 3x Worker nodes, each being:
    * 4x vCPUs, 16GB of RAM, and 40gb storage

  **Note** that this would also depend on your underlying infrastructure, and it does NOT include requirements for persistent volumes/storage.

![Mojaloop Deployment Recommendations - Infrastructure Architecture](../.gitbook/assets/KubeInfrastructureArch.svg)

### 3. Kubernetes

This section will guide the reader through the deployment process to setup Kubernetes.

If you are new to Kubernetes it is strongly recommended to familiarize yourself with Kubernetes. [Kubernetes Concepts](https://kubernetes.io/docs/concepts/overview/) is a good place to start and will provide an overview.

The following are Kubernetes concepts used within the project. An understanding of these concepts is imperative before attempting the deployment;

* Deployment
* Pod
* ReplicaSets
* Service
* Ingress
* StatefulSet
* DaemonSet
* Ingress Controller
* ConfigMap
* Secret

Insure **kubectl** is installed. A complete set of installation instruction are available [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

#### 3.1. Kubernetes Dashboard:

1. Kubernetes Dashboard roles, services & deployment.

   Install for Dashboard using Helm \(not needed if **MicroK8s** is installed\): [kubernetes-dashboard](https://github.com/helm/charts/tree/master/stable/kubernetes-dashboard)

   **IMPORTANT:** Always verify the current [kubernetes-dashboard](https://github.com/kubernetes/dashboard) yaml file is still correct as used in the below command.

   ```bash
   kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
   ```

   If you have installed MicroK8s, **enable the MicroK8s** dashboard;

   ```bash
   microk8s.enable dashboard
   ```

   **Remember** to prefix all **kubectl** commands with **microk8s** if you opted not to create an alias.

2. Verify Kubernetes Dashboard. _Windows replace `grep` with `findstr`_;

   ```bash
   kubectl get pod --namespace=kube-system |grep dashboard
   ```

3. Start proxy for local UI in new terminal;

   ```bash
   kubectl proxy ui
   ```

4. Open URI in default browser:

   ```text
   http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/
   ```

   Select **Token**. Generate a token to use there by: _Windows replace `grep` with `findstr`_

   ```bash
   kubectl describe secret kubernetes-dashboard --namespace=kube-system
   ```

   The token to use is shown on the last line of the output of that command;

   ```bash
   kubectl -n kube-system describe secrets/kubernetes-dashboard-token-btbwf
   ```

   The **{kubernetes-dashboard-token-btbwf}** is retrieved from the output in the previous step. For more information on generating the token, follow the **Authentication** link in the window.

![kubernetes-dashboard](../.gitbook/assets/kubernetesDashboard.png)

### 4. Helm

Please review [Mojaloop Helm Chart](../repositories/helm.md) to understand the relationships between the deployed Mojaloop helm charts.

Refer to the official documentation on how to install the latest version of Helm v3: [https://helm.sh/docs/intro/install/](https://helm.sh/docs/intro/install/)

Refer to the following document if are using Helm v2: [Deployment with \(Deprecated\) Helm v2](helm-legacy-deployment.md)

Refer to the [Helm v2 to v3 Migration Guide](helm-legacy-migration.md) if you wish to migrate an existing Helm v2 deployment to v3.

#### 4.1. Helm configuration

1. Add mojaloop repo to your Helm config:

   ```bash
   helm repo add mojaloop https://mojaloop.io/helm/repo/
   ```

   If the repo already exists, substitute 'add' with 'apply' in the above command.

2. Add the additional dependency Helm repositories. This is needed to resolve Helm Chart dependencies required by Mojaloop charts.

   ```bash
   helm repo add incubator http://storage.googleapis.com/kubernetes-charts-incubator
   helm repo add kiwigrid https://kiwigrid.github.io
   helm repo add elastic https://helm.elastic.co
   helm repo add bitnami https://charts.bitnami.com/bitnami
   ```

3. Update helm repositories:

   ```bash
   helm repo update
   ```

4. Optionally Install nginx-ingress for load balancing & external access:

   ```bash
   helm --namespace kube-public install stable/nginx-ingress
   ```

### 5. Mojaloop

#### 5.1. Mojaloop Helm Deployment

1. Install Mojaloop:

   Default installation:

   ```bash
   helm --namespace demo install moja mojaloop/mojaloop
   ```

   Version specific installation:

   ```bash
   helm --namespace demo install moja mojaloop/mojaloop --version {version}
   ```

   List of available versions:

   ```bash
   helm search repo -l mojaloop/mojaloop
   ```

   Custom configured installation:

   ```bash
   helm --namespace demo install moja mojaloop/mojaloop -f {custom-values.yaml}
   ```

   _Note: Download and customize the_ [_values.yaml_](https://github.com/mojaloop/helm/blob/master/mojaloop/values.yaml)_. Also ensure that you are using the value.yaml from the correct version which can be found via_ [_Helm Releases_](https://github.com/mojaloop/helm/releases)_._

#### 5.2. Verifying Mojaloop Deployment

1. Update your /etc/hosts for local deployment:

   _Note: This is only applicable for local deployments, and is not needed if custom DNS or ingress rules are configured in a customized_ [_values.yaml_](https://github.com/mojaloop/helm/blob/master/mojaloop/values.yaml).

   ```bash
   vi /etc/hosts
   ```

   _Windows the file can be updated in notepad - need to open with Administrative privileges. File location `C:\Windows\System32\drivers\etc\hosts`_.

   Include the following lines \(_or alternatively combine them_\) to the host config.

   The below required config is applicable to Helm release &gt;= versions 6.2.2 for Mojaloop API Services;

   ```text
   127.0.0.1       central-ledger.local central-settlement.local ml-api-adapter.local account-lookup-service.local account-lookup-service-admin.local quoting-service.local moja-simulator.local central-ledger central-settlement ml-api-adapter account-lookup-service account-lookup-service-admin quoting-service simulator host.docker.internal transaction-request-service.local
   ```

   The below optional config is applicable to Helm release &gt;= versions 6.2.2 for Internal components, please include the following in the host configuration.

   ```text
   127.0.0.1       forensic-logging-sidecar.local central-kms.local central-event-processor.local email-notifier.local
   ```

   For Helm legacy releases prior to versions 6.2.2, please include the following in the host configuration.

   ```text
   127.0.0.1       interop-switch.local central-end-user-registry.local central-directory.local central-hub.local
   ```

2. Test system health in your browser after installation. This will only work if you have an active helm chart deployment running.

   _Note: The examples below are only applicable to a local deployment. The entries should match the DNS values or ingress rules as configured in the_ [_values.yaml_](https://github.com/mojaloop/helm/blob/master/mojaloop/values.yaml) _or otherwise matching any custom ingress rules configured_.

   **ml-api-adapter** health test:

   ```text
   http://ml-api-adapter.local/health
   ```

   **central-ledger** health test:

   ```text
   http://central-ledger.local/health
   ```

### 6. Postman

Postman is used to send requests and receive responses.

#### 6.1. Installing Postman

Please, follow these instructions: [Get Postman](https://www.getpostman.com/postman) and install the Postman application.

#### 6.2. Setup Postman

Grab the latest collections & environment files from [Mojaloop Postman Github repo](https://github.com/mojaloop/postman).

After an initial setup or new deployment, the [OSS New Deployment FSP Setup section](../contributors-guide/tools-and-technologies/automated-testing.md) needs to be completed. This will seed the Database with the required enumerations and static data to enable the sucessful execution of any manual or automation tests by the other collections.

Refer to the [QA and Regression Testing in Mojaloop](../contributors-guide/tools-and-technologies/automated-testing.md) documentation for more complete information to complement your testing requirements.

