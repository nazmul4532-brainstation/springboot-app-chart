# Spring Boot App Helm Chart

This repository contains a Helm chart template for deploying a Spring Boot application. Below is an overview of the key components, including Deployment, StatefulSet, Service, and configuration settings.
## Package Generation

Move in the directory with Chart.yaml file and execute the following command:
```bash
cd springboot-app-chart
helm package .
```
This will generate a chart package, `spring-boot-app-chart-0.2.1.tgz`. Modify the package version in the `Chart.yaml` file.

## Application Deployment with External Values File

Using an External values files to configure the necessary configurations for the Deployment or StatefulSet, like their image, resource limitations, replicas along with their services and environment variables.

```bash
helm install <release-name> springboot-app-chart-<version>.tgz -f custom-values.yaml
```

## Key Components

### Deployment

The chart includes a **Deployment** configuration that allows you to manage stateless applications. It also consists of support for StatefulSets. Services and Environment Variables for them can be configured in the values file. You can customize the container behavior, including the number of replicas and container settings. 

### StatefulSet

To deploy a **StatefulSet**, you need to ensure that:

```yaml
  kind: StatefulSet
```
is set in your template. A StatefulSet is ideal for applications that require stable network identifiers, persistent storage, and ordered deployment and scaling.

### Service

The chart defines a **Service** to expose the application to other services within the cluster. The default configuration is as follows:

```yaml
service:
  type: ClusterIP
  targetPort: 8080
  port: 80
```

### Configure Environment Variables

The chart supports custom **ENV** via the config section in the values.yaml file. Here’s a sample configuration:

```yaml
config:
  MONGO_URL: "<URL>"
```



### Other Important Configurations 
```yaml
replicaCount: 1
image:
  repository: nginx
  pullPolicy: Always
  tag: ""

resources:
  requests:
    memory: "500Mi"
    cpu: "100m"
  limits:
    memory: "1Gi"
    cpu: "500m"
```
