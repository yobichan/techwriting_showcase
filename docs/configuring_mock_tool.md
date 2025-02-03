# About this guide

This guide helps you configure the Mockoon mock tool on your work computer.

## Target audience

This guide is intended for:

- Developers who need to mock APIs for testing
- Technical writers who need to document API behavior
- DevOps engineers who need to integrate mock APIs

# Prerequisites

Before the installation, ensure the following:

- Mockoon and Docker Desktop are installed locally
- Helm is preinstalled locally

# Installing Mockoon Desktop

To install Mockoon desktop, do the following:

1. Navigate to the official Mockoon website.
1. Download the Mockoon setup for your operating system.
1. Install Mockoon for your operating system.
1. Open Mockoon Desktop.
1. Create an exemlpary API with the official guide.
1. Right click on the example API. From the menu, select the **Copy to clipboard (JSON)** option.
1. Save the copied JSON to a folder.

# Running Mockoon Docker image

1. Download the official Docker image of Mockoon CLI:
   ```console
   docker pull mockoon/cli:latest
   ```
2. Using either the JSON file from Installing Mockoon desktop or an OpenAPI JSON file, run the mockoon-cli Docker container:

   ```console
    docker run --rm -v $(pwd)/data.json:/data -p 3000:3000 mockoon/cli:latest -d data -p 3000
   ```

# Configuring query parameters

To configure query parameters, do the following:

1. Open Mockoon Desktop.
1. Select the API endpoint you want to configure.
1. Click on the **Query Params** tab in the endpoint configuration panel.
1. Click the **Add** button to create a new query parameter.
1. Enter the **Name** and **Value** for the query parameter.
1. Optionally, set the **Default Value** and **Description** for better clarity.
1. Repeat steps 4-6 to add more query parameters as needed.
1. Save your changes by clicking the **Save** button or pressing `Ctrl+S` (Windows) or `Cmd+S` (Mac).
1. Test the configuration on port 3000 with the following path:
   `http://localhost:3000/get?path=paramA és http://http://localhost:3000/get?path=paramB`

## Example JSON response 1

```json
//Sample body
[
  "John",

  {
    "title": "Tutorial 0",
    "tags": "proxy mode"
  },
  {
    "title": "Tutorial 1",
    "tags": "templating"
  },
  {
    "title": "Tutorial 2",
    "tags": "proxy mode"
  },
  {
    "title": "Tutorial 3",
    "tags": "proxy mode,https"
  },
  {
    "title": "Tutorial 4",
    "tags": "https"
  }
]
```

## Example JSON response 2

```json
//Sample body
[
  "Jack",

  {
    "title": "Tutorial 0",
    "tags": "Getting started"
  },
  {
    "title": "Tutorial 1",
    "tags": "templating,headers,proxy mode"
  },
  {
    "title": "Tutorial 2",
    "tags": "templating,headers,proxy mode"
  },
  {
    "title": "Tutorial 3",
    "tags": "templating"
  },
  {
    "title": "Tutorial 4",
    "tags": "headers"
  }
]
```

# Deploying Mockoon to Kubernetes

This section helps you configure the Helm chart for deploying Mockoon in your Kubernetes environment.

1. Create a Helm chart:

```console
  helm create mockoon
```

2. Update the values.yaml file as follows:

```yaml
docker:
  prefix: myregistry.com/myproject
  path: mock/mockoon/cli

url:
  suffix: /api/v1

replicas: 1

targetKDE: openshift

runAsUser: 1000
runAsGroup: 1000

ports:
  mockoon: 3000

resources:
  limits:
    cpu: 1
    memory: 1Gi
  requests:
    cpu: 250m
    memory: 500Mi
```

| Variable                    | Values or range                                           |
| :-------------------------- | :-------------------------------------------------------- |
| `encodedDataJson`           | Base64 encoded string representing the custom `data.json` |
| `ports.mockoon`             | 1-65535                                                   |
| `runAsGroup`                | Rancher esetén a security context                         |
| `runAsUser`                 | The value of the security context                         |
| `targetKDE`                 | `openshift`, `rke2`                                       |
| `resources.limits.cpu`      | CPU limit (e.g., `500m` for 0.5 CPU)                      |
| `resources.limits.memory`   | Memory limit (e.g., `512Mi` for 512 MiB)                  |
| `resources.requests.cpu`    | CPU request (e.g., `250m` for 0.25 CPU)                   |
| `resources.requests.memory` | Memory request (e.g., `256Mi` for 256 MiB)                |

4. Package your Helm chart with the followign command:

```console
helm package mockoon
```

5. Deploy the Helm chart with the followign command:

```console
helm install mockoon ./mockoon-0.1.0.tgz
```

6. Verify your deployment with the following command:

```console
kubectl get pods
```

7. Access the Mockoon service on port 3000 with the following command:

```console
kubectl port-forward svc/mockoon 3000:3000
```
