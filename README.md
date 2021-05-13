# Config Connector Getting Started

Config Connector is a Kubernetes addon that allows you to manage Google Cloud resources through Kubernetes.

Config Connector provides a method to configure the following resources
- [The supported Resources](https://cloud.google.com/config-connector/docs/reference/overview)

## Description

## Demo

## Features

- feature:1
- feature:2

## Requirement
- Resouce Manager API
- GKE Add-on
- Default Namespace

### Resouce Manager API
```shell
$ gcloud services enable cloudresourcemanager.googleapis.com
```
### GKE Add-on
Create the cluster with the followings:

- Config Connector add-on
- Worload Identity
- Kubernetes Engine Monitoring

```shell
$ gcloud container clusters create config-connector-cluster \
    --addons ConfigConnector \
    --workload-pool (gcloud config get-value project).svc.id.goog \
    --enable-stackdriver-kubernetes
```

#### Service Account for Workload Identity

Create Service Account
```shell
$ gcloud iam service-accounts create shinyay-config
```

Give Service Account permissions on the Project
```
$ gcloud projects add-iam-policy-binding (gcloud config get-value project) \
    --member serviceAccount:shinyay-config@(gcloud config get-value project).iam.gserviceaccount.com \
    --role roles/owner
```

Bind **Service Account** and the predefined **Kubernetes Service Account**
```
$ gcloud iam service-accounts add-iam-policy-binding shinyay-config@(gcloud config get-value project).iam.gserviceaccount.com \
    --member serviceAccount:(gcloud config get-value project).svc.id.goog[cnrm-system/cnrm-controller-manager] \
    --role roles/iam.workloadIdentityUser
```

#### Config Connector Configuration

Replace `PROJECT_ID` to you PROJECT ID amd apply it.

configconnector.yml
```yaml
apiVersion: core.cnrm.cloud.google.com/v1beta1
kind: ConfigConnector
metadata:
  name: configconnector.core.cnrm.cloud.google.com
spec:
 mode: cluster
 googleServiceAccount: shinyay-config@<PROJECT_ID>.iam.gserviceaccount.com
```

```shell
$ kubectl apply -f configconnector.yml
```

#### Specifiy the Namespace

```shell
$ kubectl create namespace config-connector
$ kubectl annotate namespace config-connector cnrm.cloud.google.com/project-id=(gcloud config get-value project)
```

#### Verify the installation
```shell
$ kubectl wait -n cnrm-system --for=condition=Ready pod --all
```

## Usage

## Installation

## References

## Licence

Released under the [MIT license](https://gist.githubusercontent.com/shinyay/56e54ee4c0e22db8211e05e70a63247e/raw/34c6fdd50d54aa8e23560c296424aeb61599aa71/LICENSE)

## Author

[shinyay](https://github.com/shinyay)
