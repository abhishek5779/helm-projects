# Installing a CMS with Helm

In this challenge, you will learn how to install a Content Management System (CMS) using Helm. The CMS consists of two main components:

- **MySQL Database Server:** This is used to persist all data.
- **WordPress Web Server:** This exposes your content and provides a platform for easy content updates.

## Step-by-Step Installation

### Manual Installation

To manually install the CMS components, follow these steps:

1. **Install the MySQL Chart:**

    ```sh
    helm install mysql mysql-chart/ --values mysql-chart/values.yaml
    ```

2. **Install the WordPress Chart:**

    ```sh
    helm install wordpress wordpress-chart/ --values wordpress-chart/values.yaml
    ```

3. **Verify Pod Status:**

    Ensure both pods are running:

    ```sh
    kubectl get pods
    ```

4. **Get the WordPress Service URL:**

    Use Minikube to get the URL for the WordPress service:

    ```sh
    minikube service wordpress --url
    ```

    Right-click the URL and open it in your browser. It may take a moment to load.

## Congratulations!

You have successfully installed a CMS in Kubernetes using Helm.

## Managing Dependencies with Helm

WordPress requires MySQL to be installed first, as it depends on MySQL for database connections. To manage this dependency efficiently, you can use Helm's dependency management feature.

### Defining Dependencies

1. **Update the Chart.yaml File:**

    In the parent chart (e.g., WordPress), define the dependency on the MySQL chart in the `Chart.yaml` file:

    ```yaml
    dependencies:
      - name: mysql-chart
        version: 0.1.0  # Chart version
        repository: "file://../mysql-chart"
    ```

2. **Update Dependencies:**

    Run the following command to update the dependencies:

    ```sh
    helm dependency update wordpress-chart/
    ```

3. **Install the Parent Chart:**

    Now, install both applications as a whole by installing the parent chart:

    ```sh
    helm install my-release wordpress-chart/
    ```

    This approach ensures that MySQL is installed before WordPress, satisfying the dependency requirement.