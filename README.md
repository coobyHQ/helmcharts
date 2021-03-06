# The Cooby Library for Kubernetes

Forked from https://github.com/helm/charts/tree/master/stable/odoo
The Bitnami chart is enriched by several mor libraries to run more custom modules on Odoo.
The version odoo-cooby creates a all-in-one Odoo pod as the one from Bitnami does.
The version odoo-app creates only Odoo pod which holds the Odoo application server.
You need an external postgres pod to use it.

## Cooby charts
- [Odoo Cooby version](https://github.com/coobyHQ/helmcharts/tree/master/odoo-cooby)
- [Odoo App (only)](https://github.com/coobyHQ/helmcharts/tree/master/odoo-app)

## Before you begin

### Setup a Kubernetes Cluster

The quickest way to setup a Kubernetes cluster is with [Hetzner Kubernetes Service](https://cooby.cloud/blog/our-blog-1/post/building-cooby-cloud-at-hetzner-2),
For setting up Kubernetes on other cloud platforms or bare-metal servers refer to the Kubernetes [getting started guide](http://kubernetes.io/docs/getting-started-guides/).

### Install Helm

Helm is a tool for managing Kubernetes charts. Charts are packages of pre-configured Kubernetes resources.

To install Helm, refer to the [Helm install guide](https://github.com/helm/helm#install) and ensure that the `helm` binary is in the `PATH` of your shell.



### Using Helm

Once you have installed the Helm client and initialized the Tiller server, you can deploy a Bitnami Helm Chart into a Kubernetes cluster.

Please refer to the [Quick Start guide](https://github.com/helm/helm/blob/master/docs/quickstart.md) if you wish to get running in just a few commands, otherwise the [Using Helm Guide](https://github.com/helm/helm/blob/master/docs/using_helm.md) provides detailed instructions on how to use the Helm client to manage packages on your Kubernetes cluster.

Useful Helm Client Commands:
* View available charts: `helm search`
* Install a chart: `helm install stable/<package-name>`
* Upgrade your application: `helm upgrade`

# License

Forked from Bitnami Docker Odoo https://github.com/bitnami/bitnami-docker-odoo, and got heavily reshaped

Copyright 2018 Cooby tec

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

  <http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
