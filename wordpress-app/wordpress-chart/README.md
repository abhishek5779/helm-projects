# WordPress Helm Chart

## Overview

This Helm chart simplifies the deployment of a WordPress application on a Kubernetes cluster. It provides a configurable and scalable solution, allowing you to quickly provision and manage your WordPress instance.

## Features

* **WordPress Deployment:** Automates the deployment of a WordPress application.
* **Replica Management:** Easily configure the number of WordPress replicas for scaling and high availability.
* **Customizable Image:** Specify a custom WordPress image and tag to align with your specific requirements.
* **Service Account Integration:** Creates and manages a dedicated service account for enhanced security.
* **Resource Management:** Define resource requests and limits to optimize resource allocation and ensure stability.
* **Health Checks:** Implements liveness and readiness probes for automated health monitoring and recovery.
* **Ingress Support:** Optionally configure Ingress for external access to your WordPress application.
* **Persistent Storage:** Configure PersistentVolumeClaims (PVCs) for data durability.

## Directory Structure

The chart's directory structure is organized as follows:

* `Chart.yaml`: Contains metadata about the Helm chart, such as its name, version, and description.
* `values.yaml`: Contains the default configuration values for the chart.
* `templates/`: This directory holds the Kubernetes resource templates that define the WordPress deployment.
  * `_helpers.tpl`: Contains reusable template functions to simplify the resource definitions.
  * `deployment.yaml`: Defines the WordPress Deployment resource.
  * `service.yaml`: Defines the Service resource for accessing the WordPress deployment.
  * `ingress.yaml`: Defines the Ingress resource for external access.
  * `pvc.yaml`: Defines the PersistentVolumeClaim resource for persistent storage.
  * `NOTES.txt`: Provides post-installation instructions and helpful tips.

## Configuration

Customize your WordPress deployment by modifying the `values.yaml` file. Key configuration parameters include:

* `replicaCount`: The number of WordPress replicas to deploy.
* `image`: Configuration options for the WordPress image, such as the repository and tag.
* `serviceAccount`: Settings for the service account used by the deployment.
* `resources`: Resource requests and limits for the WordPress containers.
* `livenessProbe` and `readinessProbe`: Configuration for the liveness and readiness probes.
* `ingress`: Configuration for enabling and customizing Ingress.
* `persistence`: Settings for configuring PersistentVolumeClaims (PVCs) for data durability.

## Usage

1. **Install the Helm chart:**

    ```sh
    helm install my-release ./wordpress-chart
    ```
    Replace `my-release` with a name for your deployment.

2. **Customize the deployment:**

    You can customize the deployment by either editing the `values.yaml` file directly or using the `--set` flag during installation:

    ```sh
    helm install my-release ./wordpress-chart --set replicaCount=2
    ```
    This command installs the chart with `replicaCount` set to `2`.

## Notes

* Ensure that your Kubernetes cluster is up and running before installing the chart.
* Customize the WordPress credentials (username, password, database name) as needed by modifying the relevant sections in `values.yaml` or the [deployment.yaml](http://_vscodecontentref_/0) template.
* Consider using a dedicated PersistentVolumeClaim (PVC) for persistent storage to ensure data durability.

For more in-depth information about Helm, refer to the official [Helm documentation](https://helm.sh/docs/).