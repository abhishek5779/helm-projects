To set up your Helm charts as dependencies in a repository rather than using file paths, you need to follow these steps:

### Step 1: Package Your Charts

First, ensure that both your parent and child charts are correctly configured. Then, package each chart using the `helm package` command. This creates a `.tgz` file for each chart.

```bash
# Navigate to the chart directories
cd ~/parent-chart
helm package .

cd ~/child-chart
helm package .
```

This will create `parent-chart-0.1.0.tgz` and `child-chart-0.1.0.tgz` (or similar versions) in their respective directories.

### Step 2: Create a Chart Repository

You need to create a directory for your Helm chart repository and move the packaged charts there.

```bash
mkdir ~/my-helm-repo
mv ~/parent-chart/*.tgz ~/my-helm-repo/
mv ~/child-chart/*.tgz ~/my-helm-repo/
```

### Step 3: Generate an Index File

Navigate to your Helm repository directory and generate an `index.yaml` file that will serve as the metadata for the charts in your repository.

```bash
cd ~/my-helm-repo
helm repo index . --url https://your-repo-url.com/my-helm-repo
```

Replace `https://your-repo-url.com/my-helm-repo` with the actual URL where you plan to host your repository.

### Step 4: Upload the Charts to a Remote Repository

You can host your Helm repository on various platforms like GitHub Pages, AWS S3, or Google Cloud Storage. Here’s an example of how to upload your charts to a remote server:

1. **Using a web server**: If you have access to an HTTP server, upload both the `.tgz` files and `index.yaml` to the server.

2. **Using cloud storage**: If you're using AWS S3, for example, you can use the AWS CLI:

```bash
aws s3 cp ~/my-helm-repo s3://your-s3-bucket/my-helm-repo --recursive
```

### Step 5: Update Parent Chart's Dependencies

Now, update the `Chart.yaml` of the parent chart to include the child chart as a dependency using the URL of your hosted repository.

Example of `parent-chart/Chart.yaml`:

```yaml
apiVersion: v2
name: parent-chart
description: A Helm chart that depends on child-chart
version: 0.1.0

dependencies:
  - name: child-chart
    version: 0.1.0
    repository: "https://your-repo-url.com/my-helm-repo"
```

### Step 6: Update Dependencies in Parent Chart

Run the following command from within the parent chart directory to update its dependencies:

```bash
cd ~/parent-chart
helm dependency update .
```

This command will fetch the child chart from your specified repository.

### Step 7: Install the Parent Chart

Finally, you can install the parent chart, which will also install the child chart as a dependency:

```bash
helm install my-release ./parent-chart
```

By following these steps, you can effectively manage Helm charts as dependencies hosted in a remote repository, making it easier to share and deploy applications in Kubernetes environments.