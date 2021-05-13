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
- GKE Add-on
- Default Namespace
- Resouce Manager API

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
## Usage

## Installation

## References

## Licence

Released under the [MIT license](https://gist.githubusercontent.com/shinyay/56e54ee4c0e22db8211e05e70a63247e/raw/34c6fdd50d54aa8e23560c296424aeb61599aa71/LICENSE)

## Author

[shinyay](https://github.com/shinyay)
