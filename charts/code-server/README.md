# CodeServer Helm Chart

This Helm chart is a lightweight way to configure and run [code server](https://github.com/cdr/code-server).

## Requirements

- [Helm][] >=3.0.0
- Kubernetes >=1.8
- Minimum cluster requirements include the following to run this chart with
  default settings. All of these settings are configurable.
  - Three Kubernetes nodes to respect the default "hard" affinity settings
  - 1GB of RAM for the JVM heap

## Installing

You can install the helm chart via ordinary Helm process.

```bash
helm repo add kopwei https://kopwei.github.io/helm-charts
helm install cs kopwei/code-server -f <PATH/TO/YOUR/VALUES.yaml>
```

### Use your personal password

The password of code-server release changes every time if you don't have a fixed value. You may use following commands to define your own fixe password.

```bash
kubectl create secret generic codeserver --from-literal codeserver-password="<YOUR_PASSWORD>"

helm install cs kopwei/code-server --set coderserver.existingSecret=codeserver
```

## Configuration

| Parameter                   | Description                                                                                                                             | Default                |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| `affinity`                  | Configurable [affinity][]                                                                                                               | `{}`                   |
| `image.repository`          | The CoderServer Docker image                                                                                                            | `codercom/code-server` |
| `image.tag`                 | The tag of coderserver image                                                                                                            |                        |
| `fullnameOverride`          | Overrides the full name of the resources. If not set the name will default to " `.Release.Name` - `.Values.nameOverride orChart.Name` " | `""`                   |
| `image.pullPolicy`          | The Kubernetes [imagePullPolicy][]value                                                                                                 | `IfNotPresent`         |
| `imagePullSecrets`          | Configuration for [imagePullSecrets][] so that you can use a private registry for your image                                            | `[]`                   |
| `ingress`                   | Configurable [ingress][] to expose the Codeserver service.                                                                              | see [values.yaml][]    |
| `nameOverride`              | Overrides the chart name for resources. If not set the name will default to `.Chart.Name`                                               | `""`                   |
| `nodeSelector`              | Configurable [nodeSelector][] so that you can target specific nodes for your Codeserver instances                                       | `{}`                   |
| `podAnnotations`            | Configurable [annotations][] applied to all Kibana pods                                                                                 | `{}`                   |
| `podSecurityContext`        | Allows you to set the [securityContext][] for the pod                                                                                   | see [values.yaml][]    |
| `resources`                 | Allows you to set the [resources][] for the Deployment                                                                                  | see [values.yaml][]    |
| `serviceAccount`            | Allows you to overwrite the "default" [serviceAccount][] for the pod                                                                    | `[]`                   |
| `service`                   | Configurable [service][] to expose the Kibana service.                                                                                  | see [values.yaml][]    |
| `tolerations`               | Configurable [tolerations][]                                                                                                            | `[]`                   |
| `codeserver.password`       | The password of codeserver                                                                                                              | "Q!6^H~#qhB)d5(Bp"     |
| `codeserver.existingSecret` | The secret object contains password                                                                                                     | ""                     |
