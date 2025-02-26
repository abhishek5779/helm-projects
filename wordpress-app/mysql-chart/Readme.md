# MySQL Helm Chart

## Overview

This Helm chart simplifies the deployment of a MySQL database application on a Kubernetes cluster. It provides a configurable and scalable solution, allowing you to quickly provision and manage your MySQL instance.

## Features

*   **MySQL Deployment:** Automates the deployment of a MySQL database.
*   **Replica Management:** Easily configure the number of MySQL replicas for scaling and high availability.
*   **Customizable Image:** Specify a custom MySQL image and tag to align with your specific requirements.
*   **Service Account Integration:** Creates and manages a dedicated service account for enhanced security.
*   **Resource Management:** Define resource requests and limits to optimize resource allocation and ensure stability.
*   **Health Checks:** Implements liveness and readiness probes for automated health monitoring and recovery.
*   **Ingress Support:** Optionally configure Ingress for external access to your MySQL database.
*   **Autoscaling:** Supports autoscaling to dynamically adjust resources based on demand.

## Directory Structure

The chart's directory structure is organized as follows:

*   `.helmignore`: Specifies patterns to exclude when packaging the chart.
*   `Chart.yaml`: Contains metadata about the Helm chart, such as its name, version, and description.
*   `charts/`: Directory for storing chart dependencies (if any).
*   `templates/`: This directory holds the Kubernetes resource templates that define the MySQL deployment.
    *   `_helpers.tpl`: Contains reusable template functions to simplify the resource definitions.
    *   `deployment.yaml`: Defines the MySQL Deployment resource.
    *   `NOTES.txt`: Provides post-installation instructions and helpful tips.
    *   `pvc.yaml`: Defines the PersistentVolumeClaim resource for persistent storage.
    *   `service.yaml`: Defines the Service resource for accessing the MySQL deployment.
    *   `tests/`: Contains test resources for verifying the chart's functionality.
        *   `test-connection.yaml`: Defines a test Pod to verify connectivity to the MySQL database.
*   `values.yaml`: Contains the default configuration values for the chart.

## Configuration

Customize your MySQL deployment by modifying the `values.yaml` file. Key configuration parameters include:

*   `replicaCount`: The number of MySQL replicas to deploy.
*   `image`: Configuration options for the MySQL image, such as the repository and tag.
*   `serviceAccount`: Settings for the service account used by the deployment.
*   `resources`: Resource requests and limits for the MySQL containers.
*   `livenessProbe` and `readinessProbe`: Configuration for the liveness and readiness probes.
*   `autoscaling`: Settings for enabling and configuring autoscaling.
*   `ingress`: Configuration for enabling and customizing Ingress.

## Usage

1.  **Install the Helm chart:**

    ```
    helm install my-release ./mysql-chart
    ```
    Replace `my-release` with a name for your deployment.

2.  **Customize the deployment:**

    You can customize the deployment by either editing the `values.yaml` file directly or using the `--set` flag during installation:

    ```
    helm install my-release ./mysql-chart --set replicaCount=2
    ```
    This command installs the chart with `replicaCount` set to `2`.

## Notes

*   Ensure that your Kubernetes cluster is up and running before installing the chart.
*   Customize the MySQL credentials (username, password, database name) as needed by modifying the relevant sections in `values.yaml` or the `deployment.yaml` template.
*   Consider using a dedicated PersistentVolumeClaim (PVC) for persistent storage to ensure data durability.

For more in-depth information about Helm, refer to the official [Helm documentation](https://helm.sh/docs/).
