<!--- app-name: KubeRay -->

# Bitnami package for KubeRay

KubeRay is a Kubernetes operator for deploying and management of Ray applications on Kubernetes using CustomResourceDefinitions.

[Overview of KubeRay](https://ray.io)

Trademarks: This software listing is packaged by Bitnami. The respective trademarks mentioned in the offering are owned by the respective companies, and use of them does not imply any affiliation or endorsement.

## TL;DR

```console
helm install my-release oci://registry-1.docker.io/bitnamicharts/kuberay
```

Looking to use KubeRay in production? Try [VMware Tanzu Application Catalog](https://bitnami.com/enterprise), the enterprise edition of Bitnami Application Catalog.

## Introduction

This chart bootstraps a [KubeRay](https://github.com/bitnami/containers/tree/main/bitnami/kuberay) deployment on a [Kubernetes](https://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.dev/) for deployment and management of Helm Charts in clusters.

## Prerequisites

- Kubernetes 1.23+
- Helm 3.8.0+

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm install my-release REGISTRY_NAME/REPOSITORY_NAME/kuberay
```

> Note: You need to substitute the placeholders `REGISTRY_NAME` and `REPOSITORY_NAME` with a reference to your Helm chart registry and repository. For example, in the case of Bitnami, you need to use `REGISTRY_NAME=registry-1.docker.io` and `REPOSITORY_NAME=bitnamicharts`.

The command deploys kuberay on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

### Global parameters

| Name                      | Description                                     | Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `global.imageRegistry`    | Global Docker image registry                    | `""`  |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]`  |
| `global.storageClass`     | Global StorageClass for Persistent Volume(s)    | `""`  |

### Common parameters

| Name                     | Description                                                                                                                                      | Value                 |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------- |
| `kubeVersion`            | Override Kubernetes version                                                                                                                      | `""`                  |
| `nameOverride`           | String to partially override common.names.name                                                                                                   | `""`                  |
| `fullnameOverride`       | String to fully override common.names.fullname                                                                                                   | `""`                  |
| `namespaceOverride`      | String to fully override common.names.namespace                                                                                                  | `""`                  |
| `commonLabels`           | Labels to add to all deployed objects                                                                                                            | `{}`                  |
| `commonAnnotations`      | Annotations to add to all deployed objects                                                                                                       | `{}`                  |
| `clusterDomain`          | Kubernetes cluster domain name                                                                                                                   | `cluster.local`       |
| `extraDeploy`            | Array of extra objects to deploy with the release                                                                                                | `[]`                  |
| `diagnosticMode.enabled` | Enable diagnostic mode (all probes will be disabled and the command will be overridden)                                                          | `false`               |
| `diagnosticMode.command` | Command to override all containers in the deployment                                                                                             | `["sleep"]`           |
| `diagnosticMode.args`    | Args to override all containers in the deployment                                                                                                | `["infinity"]`        |
| `rayImage.registry`      | Ray registry                                                                                                                                     | `REGISTRY_NAME`       |
| `rayImage.repository`    | Ray repository                                                                                                                                   | `REPOSITORY_NAME/ray` |
| `rayImage.digest`        | Kuberay Ray digest in the way sha256:aa.... Please note this parameter, if set, will override the tag image tag (immutable tags are recommended) | `""`                  |
| `rayImage.pullPolicy`    | Kuberay Ray pull policy                                                                                                                          | `IfNotPresent`        |
| `rayImage.pullSecrets`   | Kuberay Ray pull secrets                                                                                                                         | `[]`                  |
| `rayImage.debug`         | Enable Kuberay Ray debug mode                                                                                                                    | `false`               |

### Kuberay Operator Parameters

| Name                                                         | Description                                                                                                                                                            | Value                              |
| ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| `operator.enabled`                                           | Enable Kuberay Operator                                                                                                                                                | `true`                             |
| `operator.image.registry`                                    | Kuberay Operator image registry                                                                                                                                        | `REGISTRY_NAME`                    |
| `operator.image.repository`                                  | Kuberay Operator image repository                                                                                                                                      | `REPOSITORY_NAME/kuberay-operator` |
| `operator.image.digest`                                      | Kuberay Operator image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag image tag (immutable tags are recommended)            | `""`                               |
| `operator.image.pullPolicy`                                  | Kuberay Operator image pull policy                                                                                                                                     | `IfNotPresent`                     |
| `operator.image.pullSecrets`                                 | Kuberay Operator image pull secrets                                                                                                                                    | `[]`                               |
| `operator.image.debug`                                       | Enable Kuberay Operator image debug mode                                                                                                                               | `false`                            |
| `operator.replicaCount`                                      | Number of Kuberay Operator replicas to deploy                                                                                                                          | `1`                                |
| `operator.containerPorts.metrics`                            | Kuberay Operator metrics container port                                                                                                                                | `8080`                             |
| `operator.containerPorts.health`                             | Kuberay Operator health container port                                                                                                                                 | `8082`                             |
| `operator.livenessProbe.enabled`                             | Enable livenessProbe on Kuberay Operator containers                                                                                                                    | `true`                             |
| `operator.livenessProbe.initialDelaySeconds`                 | Initial delay seconds for livenessProbe                                                                                                                                | `5`                                |
| `operator.livenessProbe.periodSeconds`                       | Period seconds for livenessProbe                                                                                                                                       | `10`                               |
| `operator.livenessProbe.timeoutSeconds`                      | Timeout seconds for livenessProbe                                                                                                                                      | `5`                                |
| `operator.livenessProbe.failureThreshold`                    | Failure threshold for livenessProbe                                                                                                                                    | `5`                                |
| `operator.livenessProbe.successThreshold`                    | Success threshold for livenessProbe                                                                                                                                    | `1`                                |
| `operator.readinessProbe.enabled`                            | Enable readinessProbe on Kuberay Operator containers                                                                                                                   | `true`                             |
| `operator.readinessProbe.initialDelaySeconds`                | Initial delay seconds for readinessProbe                                                                                                                               | `5`                                |
| `operator.readinessProbe.periodSeconds`                      | Period seconds for readinessProbe                                                                                                                                      | `10`                               |
| `operator.readinessProbe.timeoutSeconds`                     | Timeout seconds for readinessProbe                                                                                                                                     | `5`                                |
| `operator.readinessProbe.failureThreshold`                   | Failure threshold for readinessProbe                                                                                                                                   | `5`                                |
| `operator.readinessProbe.successThreshold`                   | Success threshold for readinessProbe                                                                                                                                   | `1`                                |
| `operator.startupProbe.enabled`                              | Enable startupProbe on Kuberay Operator containers                                                                                                                     | `false`                            |
| `operator.startupProbe.initialDelaySeconds`                  | Initial delay seconds for startupProbe                                                                                                                                 | `5`                                |
| `operator.startupProbe.periodSeconds`                        | Period seconds for startupProbe                                                                                                                                        | `10`                               |
| `operator.startupProbe.timeoutSeconds`                       | Timeout seconds for startupProbe                                                                                                                                       | `5`                                |
| `operator.startupProbe.failureThreshold`                     | Failure threshold for startupProbe                                                                                                                                     | `5`                                |
| `operator.startupProbe.successThreshold`                     | Success threshold for startupProbe                                                                                                                                     | `1`                                |
| `operator.customLivenessProbe`                               | Custom livenessProbe that overrides the default one                                                                                                                    | `{}`                               |
| `operator.customReadinessProbe`                              | Custom readinessProbe that overrides the default one                                                                                                                   | `{}`                               |
| `operator.customStartupProbe`                                | Custom startupProbe that overrides the default one                                                                                                                     | `{}`                               |
| `operator.watchAllNamespaces`                                | Watch for KubeRay resources in all namespaces                                                                                                                          | `true`                             |
| `operator.watchNamespaces`                                   | Watch for KubeRay resources in the given namespaces                                                                                                                    | `[]`                               |
| `operator.enableBatchScheduler`                              | Enable batch scheduler component                                                                                                                                       | `false`                            |
| `operator.resources.limits`                                  | The resources limits for the Kuberay Operator containers                                                                                                               | `{}`                               |
| `operator.resources.requests`                                | The requested resources for the Kuberay Operator containers                                                                                                            | `{}`                               |
| `operator.podSecurityContext.enabled`                        | Enabled Kuberay Operator pods' Security Context                                                                                                                        | `true`                             |
| `operator.podSecurityContext.fsGroup`                        | Set Kuberay Operator pod's Security Context fsGroup                                                                                                                    | `1001`                             |
| `operator.containerSecurityContext.enabled`                  | Enabled containers' Security Context                                                                                                                                   | `true`                             |
| `operator.containerSecurityContext.runAsUser`                | Set containers' Security Context runAsUser                                                                                                                             | `1001`                             |
| `operator.containerSecurityContext.runAsNonRoot`             | Set container's Security Context runAsNonRoot                                                                                                                          | `true`                             |
| `operator.containerSecurityContext.privileged`               | Set container's Security Context privileged                                                                                                                            | `false`                            |
| `operator.containerSecurityContext.readOnlyRootFilesystem`   | Set container's Security Context readOnlyRootFilesystem                                                                                                                | `true`                             |
| `operator.containerSecurityContext.allowPrivilegeEscalation` | Set container's Security Context allowPrivilegeEscalation                                                                                                              | `false`                            |
| `operator.containerSecurityContext.capabilities.drop`        | List of capabilities to be dropped                                                                                                                                     | `["ALL"]`                          |
| `operator.containerSecurityContext.seccompProfile.type`      | Set container's Security Context seccomp profile                                                                                                                       | `RuntimeDefault`                   |
| `operator.command`                                           | Override default container command (useful when using custom images)                                                                                                   | `[]`                               |
| `operator.args`                                              | Override default container args (useful when using custom images)                                                                                                      | `[]`                               |
| `operator.hostAliases`                                       | Kuberay Operator pods host aliases                                                                                                                                     | `[]`                               |
| `operator.podLabels`                                         | Extra labels for Kuberay Operator pods                                                                                                                                 | `{}`                               |
| `operator.podAnnotations`                                    | Annotations for Kuberay Operator pods                                                                                                                                  | `{}`                               |
| `operator.podAffinityPreset`                                 | Pod affinity preset. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                                                                             | `""`                               |
| `operator.podAntiAffinityPreset`                             | Pod anti-affinity preset. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                                                                        | `soft`                             |
| `operator.pdb.create`                                        | Enable/disable a Pod Disruption Budget creation                                                                                                                        | `false`                            |
| `operator.pdb.minAvailable`                                  | Minimum number/percentage of pods that should remain scheduled                                                                                                         | `1`                                |
| `operator.pdb.maxUnavailable`                                | Maximum number/percentage of pods that may be made unavailable                                                                                                         | `""`                               |
| `operator.nodeAffinityPreset.type`                           | Node affinity preset type. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                                                                       | `""`                               |
| `operator.nodeAffinityPreset.key`                            | Node label key to match. Ignored if `server.affinity` is set                                                                                                           | `""`                               |
| `operator.nodeAffinityPreset.values`                         | Node label values to match. Ignored if `server.affinity` is set                                                                                                        | `[]`                               |
| `operator.affinity`                                          | Affinity for Kuberay Operator pods assignment                                                                                                                          | `{}`                               |
| `operator.nodeSelector`                                      | Node labels for Kuberay Operator pods assignment                                                                                                                       | `{}`                               |
| `operator.tolerations`                                       | Tolerations for Kuberay Operator pods assignment                                                                                                                       | `[]`                               |
| `operator.updateStrategy.type`                               | Kuberay Operator statefulset strategy type                                                                                                                             | `RollingUpdate`                    |
| `operator.priorityClassName`                                 | Kuberay Operator pods' priorityClassName                                                                                                                               | `""`                               |
| `operator.topologySpreadConstraints`                         | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template                                               | `[]`                               |
| `operator.schedulerName`                                     | Name of the k8s scheduler (other than default) for Kuberay Operator pods                                                                                               | `""`                               |
| `operator.terminationGracePeriodSeconds`                     | Seconds Redmine pod needs to terminate gracefully                                                                                                                      | `""`                               |
| `operator.lifecycleHooks`                                    | for the Kuberay Operator container(s) to automate configuration before or after startup                                                                                | `{}`                               |
| `operator.extraEnvVars`                                      | Array with extra environment variables to add to Kuberay Operator nodes                                                                                                | `[]`                               |
| `operator.extraEnvVarsCM`                                    | Name of existing ConfigMap containing extra env vars for Kuberay Operator nodes                                                                                        | `""`                               |
| `operator.extraEnvVarsSecret`                                | Name of existing Secret containing extra env vars for Kuberay Operator nodes                                                                                           | `""`                               |
| `operator.extraVolumes`                                      | Optionally specify extra list of additional volumes for the Kuberay Operator pod(s)                                                                                    | `[]`                               |
| `operator.extraVolumeMounts`                                 | Optionally specify extra list of additional volumeMounts for the Kuberay Operator container(s)                                                                         | `[]`                               |
| `operator.sidecars`                                          | Add additional sidecar containers to the Kuberay Operator pod(s)                                                                                                       | `[]`                               |
| `operator.initContainers`                                    | Add additional init containers to the Kuberay Operator pod(s)                                                                                                          | `[]`                               |
| `operator.autoscaling.vpa.enabled`                           | Enable VPA                                                                                                                                                             | `false`                            |
| `operator.autoscaling.vpa.annotations`                       | Annotations for VPA resource                                                                                                                                           | `{}`                               |
| `operator.autoscaling.vpa.controlledResources`               | VPA List of resources that the vertical pod autoscaler can control. Defaults to cpu and memory                                                                         | `[]`                               |
| `operator.autoscaling.vpa.maxAllowed`                        | VPA Max allowed resources for the pod                                                                                                                                  | `{}`                               |
| `operator.autoscaling.vpa.minAllowed`                        | VPA Min allowed resources for the pod                                                                                                                                  | `{}`                               |
| `operator.autoscaling.vpa.updatePolicy.updateMode`           | Autoscaling update policy Specifies whether recommended updates are applied when a Pod is started and whether recommended updates are applied during the life of a Pod | `Auto`                             |
| `operator.autoscaling.hpa.enabled`                           | Enable autoscaling for operator                                                                                                                                        | `false`                            |
| `operator.autoscaling.hpa.minReplicas`                       | Minimum number of operator replicas                                                                                                                                    | `""`                               |
| `operator.autoscaling.hpa.maxReplicas`                       | Maximum number of operator replicas                                                                                                                                    | `""`                               |
| `operator.autoscaling.hpa.targetCPU`                         | Target CPU utilization percentage                                                                                                                                      | `""`                               |
| `operator.autoscaling.hpa.targetMemory`                      | Target Memory utilization percentage                                                                                                                                   | `""`                               |

### Kuberay Operator Traffic Exposure Parameters

| Name                                        | Description                                                                                                                      | Value                    |
| ------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------ |
| `operator.service.type`                     | Kuberay Operator service type                                                                                                    | `ClusterIP`              |
| `operator.service.ports.metrics`            | Kuberay Operator service HTTP port                                                                                               | `80`                     |
| `operator.service.nodePorts.metrics`        | Node port for HTTP                                                                                                               | `""`                     |
| `operator.service.clusterIP`                | Kuberay Operator service Cluster IP                                                                                              | `""`                     |
| `operator.service.loadBalancerIP`           | Kuberay Operator service Load Balancer IP                                                                                        | `""`                     |
| `operator.service.loadBalancerSourceRanges` | Kuberay Operator service Load Balancer sources                                                                                   | `[]`                     |
| `operator.service.externalTrafficPolicy`    | Kuberay Operator service external traffic policy                                                                                 | `Cluster`                |
| `operator.service.annotations`              | Additional custom annotations for Kuberay Operator service                                                                       | `{}`                     |
| `operator.service.extraPorts`               | Extra ports to expose in Kuberay Operator service (normally used with the `sidecars` value)                                      | `[]`                     |
| `operator.service.sessionAffinity`          | Control where web requests go, to the same pod or round-robin                                                                    | `None`                   |
| `operator.service.sessionAffinityConfig`    | Additional settings for the sessionAffinity                                                                                      | `{}`                     |
| `operator.ingress.enabled`                  | Enable ingress record generation for Kuberay                                                                                     | `false`                  |
| `operator.ingress.pathType`                 | Ingress path type                                                                                                                | `ImplementationSpecific` |
| `operator.ingress.apiVersion`               | Force Ingress API version (automatically detected if not set)                                                                    | `""`                     |
| `operator.ingress.hostname`                 | Default host for the ingress record                                                                                              | `kuberay-operator.local` |
| `operator.ingress.ingressClassName`         | IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+)                                                    | `""`                     |
| `operator.ingress.path`                     | Default path for the ingress record                                                                                              | `/`                      |
| `operator.ingress.annotations`              | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`                     |
| `operator.ingress.tls`                      | Enable TLS configuration for the host defined at `client.ingress.hostname` parameter                                             | `false`                  |
| `operator.ingress.selfSigned`               | Create a TLS secret for this ingress record using self-signed certificates generated by Helm                                     | `false`                  |
| `operator.ingress.extraHosts`               | An array with additional hostname(s) to be covered with the ingress record                                                       | `[]`                     |
| `operator.ingress.extraPaths`               | An array with additional arbitrary paths that may need to be added to the ingress under the main host                            | `[]`                     |
| `operator.ingress.extraTls`                 | TLS configuration for additional hostname(s) to be covered with this ingress record                                              | `[]`                     |
| `operator.ingress.secrets`                  | Custom TLS certificates as secrets                                                                                               | `[]`                     |
| `operator.ingress.extraRules`               | Additional rules to be covered with this ingress record                                                                          | `[]`                     |

### Kuberay Operator RBAC Parameters

| Name                                                   | Description                                                      | Value  |
| ------------------------------------------------------ | ---------------------------------------------------------------- | ------ |
| `operator.rbac.create`                                 | Specifies whether RBAC resources should be created               | `true` |
| `operator.rbac.rules`                                  | Custom RBAC rules to set                                         | `[]`   |
| `operator.serviceAccount.create`                       | Specifies whether a ServiceAccount should be created             | `true` |
| `operator.serviceAccount.name`                         | The name of the ServiceAccount to use.                           | `""`   |
| `operator.serviceAccount.annotations`                  | Additional Service Account annotations (evaluated as a template) | `{}`   |
| `operator.serviceAccount.automountServiceAccountToken` | Automount service account token for the server service account   | `true` |

### Kuberay Operator Metrics Parameters

| Name                                                | Description                                                                                            | Value   |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------- |
| `operator.metrics.enabled`                          | Enable the export of Prometheus metrics                                                                | `false` |
| `operator.metrics.annotations`                      | Annotations for the server service in order to scrape metrics                                          | `{}`    |
| `operator.metrics.serviceMonitor.enabled`           | if `true`, creates a Prometheus Operator ServiceMonitor (also requires `metrics.enabled` to be `true`) | `false` |
| `operator.metrics.serviceMonitor.namespace`         | Namespace in which Prometheus is running                                                               | `""`    |
| `operator.metrics.serviceMonitor.annotations`       | Additional custom annotations for the ServiceMonitor                                                   | `{}`    |
| `operator.metrics.serviceMonitor.labels`            | Extra labels for the ServiceMonitor                                                                    | `{}`    |
| `operator.metrics.serviceMonitor.jobLabel`          | The name of the label on the target service to use as the job name in Prometheus                       | `""`    |
| `operator.metrics.serviceMonitor.honorLabels`       | honorLabels chooses the metric's labels on collisions with target labels                               | `false` |
| `operator.metrics.serviceMonitor.interval`          | Interval at which metrics should be scraped.                                                           | `""`    |
| `operator.metrics.serviceMonitor.scrapeTimeout`     | Timeout after which the scrape is ended                                                                | `""`    |
| `operator.metrics.serviceMonitor.metricRelabelings` | Specify additional relabeling of metrics                                                               | `[]`    |
| `operator.metrics.serviceMonitor.relabelings`       | Specify general relabeling                                                                             | `[]`    |
| `operator.metrics.serviceMonitor.selector`          | Prometheus instance selector labels                                                                    | `{}`    |

### Kuberay API Server Parameters

| Name                                                          | Description                                                                                                                                                            | Value                               |
| ------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `apiserver.enabled`                                           | Enable Kuberay API Server                                                                                                                                              | `true`                              |
| `apiserver.image.registry`                                    | Kuberay API Server image registry                                                                                                                                      | `REGISTRY_NAME`                     |
| `apiserver.image.repository`                                  | Kuberay API Server image repository                                                                                                                                    | `REPOSITORY_NAME/kuberay-apiserver` |
| `apiserver.image.digest`                                      | Kuberay API Server image digest in the way sha256:aa.... Please note this parameter, if set, will override the tag image tag (immutable tags are recommended)          | `""`                                |
| `apiserver.image.pullPolicy`                                  | Kuberay API Server image pull policy                                                                                                                                   | `IfNotPresent`                      |
| `apiserver.image.pullSecrets`                                 | Kuberay API Server image pull secrets                                                                                                                                  | `[]`                                |
| `apiserver.image.debug`                                       | Enable Kuberay API Server image debug mode                                                                                                                             | `false`                             |
| `apiserver.replicaCount`                                      | Number of Kuberay API Server replicas to deploy                                                                                                                        | `1`                                 |
| `apiserver.containerPorts.http`                               | Kuberay API Server http container port                                                                                                                                 | `8888`                              |
| `apiserver.containerPorts.grpc`                               | Kuberay API Server internal (HTTPS) container port                                                                                                                     | `8887`                              |
| `apiserver.livenessProbe.enabled`                             | Enable livenessProbe on Kuberay API Server containers                                                                                                                  | `true`                              |
| `apiserver.livenessProbe.initialDelaySeconds`                 | Initial delay seconds for livenessProbe                                                                                                                                | `5`                                 |
| `apiserver.livenessProbe.periodSeconds`                       | Period seconds for livenessProbe                                                                                                                                       | `10`                                |
| `apiserver.livenessProbe.timeoutSeconds`                      | Timeout seconds for livenessProbe                                                                                                                                      | `5`                                 |
| `apiserver.livenessProbe.failureThreshold`                    | Failure threshold for livenessProbe                                                                                                                                    | `5`                                 |
| `apiserver.livenessProbe.successThreshold`                    | Success threshold for livenessProbe                                                                                                                                    | `1`                                 |
| `apiserver.readinessProbe.enabled`                            | Enable readinessProbe on Kuberay API Server containers                                                                                                                 | `true`                              |
| `apiserver.readinessProbe.initialDelaySeconds`                | Initial delay seconds for readinessProbe                                                                                                                               | `5`                                 |
| `apiserver.readinessProbe.periodSeconds`                      | Period seconds for readinessProbe                                                                                                                                      | `10`                                |
| `apiserver.readinessProbe.timeoutSeconds`                     | Timeout seconds for readinessProbe                                                                                                                                     | `5`                                 |
| `apiserver.readinessProbe.failureThreshold`                   | Failure threshold for readinessProbe                                                                                                                                   | `5`                                 |
| `apiserver.readinessProbe.successThreshold`                   | Success threshold for readinessProbe                                                                                                                                   | `1`                                 |
| `apiserver.startupProbe.enabled`                              | Enable startupProbe on Kuberay API Server containers                                                                                                                   | `false`                             |
| `apiserver.startupProbe.initialDelaySeconds`                  | Initial delay seconds for startupProbe                                                                                                                                 | `5`                                 |
| `apiserver.startupProbe.periodSeconds`                        | Period seconds for startupProbe                                                                                                                                        | `10`                                |
| `apiserver.startupProbe.timeoutSeconds`                       | Timeout seconds for startupProbe                                                                                                                                       | `5`                                 |
| `apiserver.startupProbe.failureThreshold`                     | Failure threshold for startupProbe                                                                                                                                     | `5`                                 |
| `apiserver.startupProbe.successThreshold`                     | Success threshold for startupProbe                                                                                                                                     | `1`                                 |
| `apiserver.customLivenessProbe`                               | Custom livenessProbe that overrides the default one                                                                                                                    | `{}`                                |
| `apiserver.customReadinessProbe`                              | Custom readinessProbe that overrides the default one                                                                                                                   | `{}`                                |
| `apiserver.customStartupProbe`                                | Custom startupProbe that overrides the default one                                                                                                                     | `{}`                                |
| `apiserver.watchAllNamespaces`                                | Watch for KubeRay resources in all namespaces                                                                                                                          | `true`                              |
| `apiserver.watchNamespaces`                                   | Watch for KubeRay resources in the given namespaces                                                                                                                    | `[]`                                |
| `apiserver.resources.limits`                                  | The resources limits for the Kuberay API Server containers                                                                                                             | `{}`                                |
| `apiserver.resources.requests`                                | The requested resources for the Kuberay API Server containers                                                                                                          | `{}`                                |
| `apiserver.podSecurityContext.enabled`                        | Enabled Kuberay API Server pods' Security Context                                                                                                                      | `true`                              |
| `apiserver.podSecurityContext.fsGroup`                        | Set Kuberay API Server pod's Security Context fsGroup                                                                                                                  | `1001`                              |
| `apiserver.containerSecurityContext.enabled`                  | Enabled containers' Security Context                                                                                                                                   | `true`                              |
| `apiserver.containerSecurityContext.runAsUser`                | Set containers' Security Context runAsUser                                                                                                                             | `1001`                              |
| `apiserver.containerSecurityContext.runAsNonRoot`             | Set container's Security Context runAsNonRoot                                                                                                                          | `true`                              |
| `apiserver.containerSecurityContext.privileged`               | Set container's Security Context privileged                                                                                                                            | `false`                             |
| `apiserver.containerSecurityContext.readOnlyRootFilesystem`   | Set container's Security Context readOnlyRootFilesystem                                                                                                                | `true`                              |
| `apiserver.containerSecurityContext.allowPrivilegeEscalation` | Set container's Security Context allowPrivilegeEscalation                                                                                                              | `false`                             |
| `apiserver.containerSecurityContext.capabilities.drop`        | List of capabilities to be dropped                                                                                                                                     | `["ALL"]`                           |
| `apiserver.containerSecurityContext.seccompProfile.type`      | Set container's Security Context seccomp profile                                                                                                                       | `RuntimeDefault`                    |
| `apiserver.command`                                           | Override default container command (useful when using custom images)                                                                                                   | `[]`                                |
| `apiserver.args`                                              | Override default container args (useful when using custom images)                                                                                                      | `[]`                                |
| `apiserver.hostAliases`                                       | Kuberay API Server pods host aliases                                                                                                                                   | `[]`                                |
| `apiserver.podLabels`                                         | Extra labels for Kuberay API Server pods                                                                                                                               | `{}`                                |
| `apiserver.podAnnotations`                                    | Annotations for Kuberay API Server pods                                                                                                                                | `{}`                                |
| `apiserver.podAffinityPreset`                                 | Pod affinity preset. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                                                                             | `""`                                |
| `apiserver.podAntiAffinityPreset`                             | Pod anti-affinity preset. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                                                                        | `soft`                              |
| `apiserver.pdb.create`                                        | Enable/disable a Pod Disruption Budget creation                                                                                                                        | `false`                             |
| `apiserver.pdb.minAvailable`                                  | Minimum number/percentage of pods that should remain scheduled                                                                                                         | `1`                                 |
| `apiserver.pdb.maxUnavailable`                                | Maximum number/percentage of pods that may be made unavailable                                                                                                         | `""`                                |
| `apiserver.nodeAffinityPreset.type`                           | Node affinity preset type. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                                                                       | `""`                                |
| `apiserver.nodeAffinityPreset.key`                            | Node label key to match. Ignored if `server.affinity` is set                                                                                                           | `""`                                |
| `apiserver.nodeAffinityPreset.values`                         | Node label values to match. Ignored if `server.affinity` is set                                                                                                        | `[]`                                |
| `apiserver.affinity`                                          | Affinity for Kuberay API Server pods assignment                                                                                                                        | `{}`                                |
| `apiserver.nodeSelector`                                      | Node labels for Kuberay API Server pods assignment                                                                                                                     | `{}`                                |
| `apiserver.tolerations`                                       | Tolerations for Kuberay API Server pods assignment                                                                                                                     | `[]`                                |
| `apiserver.updateStrategy.type`                               | Kuberay API Server statefulset strategy type                                                                                                                           | `RollingUpdate`                     |
| `apiserver.priorityClassName`                                 | Kuberay API Server pods' priorityClassName                                                                                                                             | `""`                                |
| `apiserver.topologySpreadConstraints`                         | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template                                               | `[]`                                |
| `apiserver.schedulerName`                                     | Name of the k8s scheduler (other than default) for Kuberay API Server pods                                                                                             | `""`                                |
| `apiserver.terminationGracePeriodSeconds`                     | Seconds Redmine pod needs to terminate gracefully                                                                                                                      | `""`                                |
| `apiserver.lifecycleHooks`                                    | for the Kuberay API Server container(s) to automate configuration before or after startup                                                                              | `{}`                                |
| `apiserver.extraEnvVars`                                      | Array with extra environment variables to add to Kuberay API Server nodes                                                                                              | `[]`                                |
| `apiserver.extraEnvVarsCM`                                    | Name of existing ConfigMap containing extra env vars for Kuberay API Server nodes                                                                                      | `""`                                |
| `apiserver.extraEnvVarsSecret`                                | Name of existing Secret containing extra env vars for Kuberay API Server nodes                                                                                         | `""`                                |
| `apiserver.extraVolumes`                                      | Optionally specify extra list of additional volumes for the Kuberay API Server pod(s)                                                                                  | `[]`                                |
| `apiserver.extraVolumeMounts`                                 | Optionally specify extra list of additional volumeMounts for the Kuberay API Server container(s)                                                                       | `[]`                                |
| `apiserver.sidecars`                                          | Add additional sidecar containers to the Kuberay API Server pod(s)                                                                                                     | `[]`                                |
| `apiserver.initContainers`                                    | Add additional init containers to the Kuberay API Server pod(s)                                                                                                        | `[]`                                |
| `apiserver.autoscaling.vpa.enabled`                           | Enable VPA                                                                                                                                                             | `false`                             |
| `apiserver.autoscaling.vpa.annotations`                       | Annotations for VPA resource                                                                                                                                           | `{}`                                |
| `apiserver.autoscaling.vpa.controlledResources`               | VPA List of resources that the vertical pod autoscaler can control. Defaults to cpu and memory                                                                         | `[]`                                |
| `apiserver.autoscaling.vpa.maxAllowed`                        | VPA Max allowed resources for the pod                                                                                                                                  | `{}`                                |
| `apiserver.autoscaling.vpa.minAllowed`                        | VPA Min allowed resources for the pod                                                                                                                                  | `{}`                                |
| `apiserver.autoscaling.vpa.updatePolicy.updateMode`           | Autoscaling update policy Specifies whether recommended updates are applied when a Pod is started and whether recommended updates are applied during the life of a Pod | `Auto`                              |
| `apiserver.autoscaling.hpa.enabled`                           | Enable autoscaling for apiserver                                                                                                                                       | `false`                             |
| `apiserver.autoscaling.hpa.minReplicas`                       | Minimum number of apiserver replicas                                                                                                                                   | `""`                                |
| `apiserver.autoscaling.hpa.maxReplicas`                       | Maximum number of apiserver replicas                                                                                                                                   | `""`                                |
| `apiserver.autoscaling.hpa.targetCPU`                         | Target CPU utilization percentage                                                                                                                                      | `""`                                |
| `apiserver.autoscaling.hpa.targetMemory`                      | Target Memory utilization percentage                                                                                                                                   | `""`                                |

### Kuberay API Server Traffic Exposure Parameters

| Name                                         | Description                                                                                                                      | Value                     |
| -------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `apiserver.service.type`                     | Kuberay API Server service type                                                                                                  | `ClusterIP`               |
| `apiserver.service.ports.http`               | Kuberay API Server service HTTP port                                                                                             | `80`                      |
| `apiserver.service.ports.grpc`               | Kuberay API Server service HTTP port                                                                                             | `8887`                    |
| `apiserver.service.nodePorts.http`           | Node port for HTTP                                                                                                               | `""`                      |
| `apiserver.service.nodePorts.grpc`           | Node port for GRPC                                                                                                               | `""`                      |
| `apiserver.service.clusterIP`                | Kuberay API Server service Cluster IP                                                                                            | `""`                      |
| `apiserver.service.loadBalancerIP`           | Kuberay API Server service Load Balancer IP                                                                                      | `""`                      |
| `apiserver.service.loadBalancerSourceRanges` | Kuberay API Server service Load Balancer sources                                                                                 | `[]`                      |
| `apiserver.service.externalTrafficPolicy`    | Kuberay API Server service external traffic policy                                                                               | `Cluster`                 |
| `apiserver.service.annotations`              | Additional custom annotations for Kuberay API Server service                                                                     | `{}`                      |
| `apiserver.service.extraPorts`               | Extra ports to expose in Kuberay API Server service (normally used with the `sidecars` value)                                    | `[]`                      |
| `apiserver.service.sessionAffinity`          | Control where web requests go, to the same pod or round-robin                                                                    | `None`                    |
| `apiserver.service.sessionAffinityConfig`    | Additional settings for the sessionAffinity                                                                                      | `{}`                      |
| `apiserver.ingress.enabled`                  | Enable ingress record generation for Kuberay                                                                                     | `false`                   |
| `apiserver.ingress.pathType`                 | Ingress path type                                                                                                                | `ImplementationSpecific`  |
| `apiserver.ingress.apiVersion`               | Force Ingress API version (automatically detected if not set)                                                                    | `""`                      |
| `apiserver.ingress.hostname`                 | Default host for the ingress record                                                                                              | `kuberay-apiserver.local` |
| `apiserver.ingress.ingressClassName`         | IngressClass that will be be used to implement the Ingress (Kubernetes 1.18+)                                                    | `""`                      |
| `apiserver.ingress.path`                     | Default path for the ingress record                                                                                              | `/`                       |
| `apiserver.ingress.annotations`              | Additional annotations for the Ingress resource. To enable certificate autogeneration, place here your cert-manager annotations. | `{}`                      |
| `apiserver.ingress.tls`                      | Enable TLS configuration for the host defined at `client.ingress.hostname` parameter                                             | `false`                   |
| `apiserver.ingress.selfSigned`               | Create a TLS secret for this ingress record using self-signed certificates generated by Helm                                     | `false`                   |
| `apiserver.ingress.extraHosts`               | An array with additional hostname(s) to be covered with the ingress record                                                       | `[]`                      |
| `apiserver.ingress.extraPaths`               | An array with additional arbitrary paths that may need to be added to the ingress under the main host                            | `[]`                      |
| `apiserver.ingress.extraTls`                 | TLS configuration for additional hostname(s) to be covered with this ingress record                                              | `[]`                      |
| `apiserver.ingress.secrets`                  | Custom TLS certificates as secrets                                                                                               | `[]`                      |
| `apiserver.ingress.extraRules`               | Additional rules to be covered with this ingress record                                                                          | `[]`                      |

### Kuberay API Server RBAC Parameters

| Name                                                    | Description                                                      | Value  |
| ------------------------------------------------------- | ---------------------------------------------------------------- | ------ |
| `apiserver.rbac.create`                                 | Specifies whether RBAC resources should be created               | `true` |
| `apiserver.rbac.rules`                                  | Custom RBAC rules to set                                         | `[]`   |
| `apiserver.serviceAccount.create`                       | Specifies whether a ServiceAccount should be created             | `true` |
| `apiserver.serviceAccount.name`                         | The name of the ServiceAccount to use.                           | `""`   |
| `apiserver.serviceAccount.annotations`                  | Additional Service Account annotations (evaluated as a template) | `{}`   |
| `apiserver.serviceAccount.automountServiceAccountToken` | Automount service account token for the server service account   | `true` |

### Kuberay API Server Metrics Parameters

| Name                                                 | Description                                                                                              | Value   |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------- | ------- |
| `apiserver.metrics.enabled`                          | Enable the export of Prometheus metrics                                                                  | `false` |
| `apiserver.metrics.annotations`                      | Annotations for the server service in order to scrape metrics                                            | `{}`    |
| `apiserver.metrics.serviceMonitor.enabled`           | if `true`, creates a Prometheus API Server ServiceMonitor (also requires `metrics.enabled` to be `true`) | `false` |
| `apiserver.metrics.serviceMonitor.namespace`         | Namespace in which Prometheus is running                                                                 | `""`    |
| `apiserver.metrics.serviceMonitor.annotations`       | Additional custom annotations for the ServiceMonitor                                                     | `{}`    |
| `apiserver.metrics.serviceMonitor.labels`            | Extra labels for the ServiceMonitor                                                                      | `{}`    |
| `apiserver.metrics.serviceMonitor.jobLabel`          | The name of the label on the target service to use as the job name in Prometheus                         | `""`    |
| `apiserver.metrics.serviceMonitor.honorLabels`       | honorLabels chooses the metric's labels on collisions with target labels                                 | `false` |
| `apiserver.metrics.serviceMonitor.interval`          | Interval at which metrics should be scraped.                                                             | `""`    |
| `apiserver.metrics.serviceMonitor.scrapeTimeout`     | Timeout after which the scrape is ended                                                                  | `""`    |
| `apiserver.metrics.serviceMonitor.metricRelabelings` | Specify additional relabeling of metrics                                                                 | `[]`    |
| `apiserver.metrics.serviceMonitor.relabelings`       | Specify general relabeling                                                                               | `[]`    |
| `apiserver.metrics.serviceMonitor.selector`          | Prometheus instance selector labels                                                                      | `{}`    |

### Ray Cluster Parameters

| Name                  | Description              | Value          |
| --------------------- | ------------------------ | -------------- |
| `cluster.enabled`     | Deploy Ray Cluster       | `true`         |
| `cluster.serviceType` | Set cluster service type | `LoadBalancer` |

### Ray Cluster Head Parameters

| Name                                                             | Description                                                                                                              | Value            |
| ---------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ---------------- |
| `cluster.head.rayStartParams`                                    | Set Ray start parameters                                                                                                 | `{}`             |
| `cluster.head.resources.limits`                                  | The resources limits for the Ray Cluster Worker (common) containers                                                      | `{}`             |
| `cluster.head.resources.requests`                                | The requested resources for the Ray Cluster Worker (common) containers                                                   | `{}`             |
| `cluster.head.podSecurityContext.enabled`                        | Enabled Ray Cluster Worker (common) pods' Security Context                                                               | `true`           |
| `cluster.head.podSecurityContext.fsGroup`                        | Set Ray Cluster Worker (common) pod's Security Context fsGroup                                                           | `1001`           |
| `cluster.head.containerSecurityContext.enabled`                  | Enabled containers' Security Context                                                                                     | `true`           |
| `cluster.head.containerSecurityContext.runAsUser`                | Set containers' Security Context runAsUser                                                                               | `1001`           |
| `cluster.head.containerSecurityContext.runAsNonRoot`             | Set container's Security Context runAsNonRoot                                                                            | `true`           |
| `cluster.head.containerSecurityContext.privileged`               | Set container's Security Context privileged                                                                              | `false`          |
| `cluster.head.containerSecurityContext.readOnlyRootFilesystem`   | Set container's Security Context readOnlyRootFilesystem                                                                  | `true`           |
| `cluster.head.containerSecurityContext.allowPrivilegeEscalation` | Set container's Security Context allowPrivilegeEscalation                                                                | `false`          |
| `cluster.head.containerSecurityContext.capabilities.drop`        | List of capabilities to be dropped                                                                                       | `["ALL"]`        |
| `cluster.head.containerSecurityContext.seccompProfile.type`      | Set container's Security Context seccomp profile                                                                         | `RuntimeDefault` |
| `cluster.head.command`                                           | Override default container command (useful when using custom images)                                                     | `[]`             |
| `cluster.head.args`                                              | Override default container args (useful when using custom images)                                                        | `[]`             |
| `cluster.head.hostAliases`                                       | Ray Cluster Worker (common) pods host aliases                                                                            | `[]`             |
| `cluster.head.podLabels`                                         | Extra labels for Ray Cluster Worker (common) pods                                                                        | `{}`             |
| `cluster.head.podAnnotations`                                    | Annotations for Ray Cluster Worker (common) pods                                                                         | `{}`             |
| `cluster.head.podAffinityPreset`                                 | Pod affinity preset. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                               | `""`             |
| `cluster.head.podAntiAffinityPreset`                             | Pod anti-affinity preset. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                          | `soft`           |
| `cluster.head.nodeAffinityPreset.type`                           | Node affinity preset type. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                         | `""`             |
| `cluster.head.nodeAffinityPreset.key`                            | Node label key to match. Ignored if `server.affinity` is set                                                             | `""`             |
| `cluster.head.nodeAffinityPreset.values`                         | Node label values to match. Ignored if `server.affinity` is set                                                          | `[]`             |
| `cluster.head.affinity`                                          | Affinity for Ray Cluster Worker (common) pods assignment                                                                 | `{}`             |
| `cluster.head.nodeSelector`                                      | Node labels for Ray Cluster Worker (common) pods assignment                                                              | `{}`             |
| `cluster.head.tolerations`                                       | Tolerations for Ray Cluster Worker (common) pods assignment                                                              | `[]`             |
| `cluster.head.priorityClassName`                                 | Ray Cluster Worker (common) pods' priorityClassName                                                                      | `""`             |
| `cluster.head.topologySpreadConstraints`                         | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template | `[]`             |
| `cluster.head.schedulerName`                                     | Name of the k8s scheduler (other than default) for Ray Cluster Worker (common) pods                                      | `""`             |
| `cluster.head.terminationGracePeriodSeconds`                     | Seconds Redmine pod needs to terminate gracefully                                                                        | `""`             |
| `cluster.head.lifecycleHooks`                                    | for the Ray Cluster Worker (common) container(s) to automate configuration before or after startup                       | `{}`             |
| `cluster.head.extraEnvVars`                                      | Array with extra environment variables to add to Ray Cluster Worker (common) nodes                                       | `[]`             |
| `cluster.head.extraEnvVarsCM`                                    | Name of existing ConfigMap containing extra env vars for Ray Cluster Worker (common) nodes                               | `""`             |
| `cluster.head.extraEnvVarsSecret`                                | Name of existing Secret containing extra env vars for Ray Cluster Worker (common) nodes                                  | `""`             |
| `cluster.head.extraVolumes`                                      | Optionally specify extra list of additional volumes for the Ray Cluster Worker (common) pod(s)                           | `[]`             |
| `cluster.head.extraVolumeMounts`                                 | Optionally specify extra list of additional volumeMounts for the Ray Cluster Worker (common) container(s)                | `[]`             |
| `cluster.head.sidecars`                                          | Add additional sidecar containers to the Ray Cluster Worker (common) pod(s)                                              | `[]`             |
| `cluster.head.initContainers`                                    | Add additional init containers to the Ray Cluster Worker (common) pod(s)                                                 | `[]`             |
| `cluster.head.customLivenessProbe`                               | Custom livenessProbe that overrides the default one                                                                      | `{}`             |
| `cluster.head.customReadinessProbe`                              | Custom readinessProbe that overrides the default one                                                                     | `{}`             |
| `cluster.head.customStartupProbe`                                | Custom startupProbe that overrides the default one                                                                       | `{}`             |

### Ray Cluster Worker Parameters

| Name                                                                      | Description                                                                                                              | Value            |
| ------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------ | ---------------- |
| `cluster.worker.common.rayStartParams`                                    | Set Ray start parameters                                                                                                 | `{}`             |
| `cluster.worker.common.replicaCount`                                      | Number of Ray Cluster Worker (common) replicas to deploy                                                                 | `1`              |
| `cluster.worker.common.customLivenessProbe`                               | Custom livenessProbe that overrides the default one                                                                      | `{}`             |
| `cluster.worker.common.customReadinessProbe`                              | Custom readinessProbe that overrides the default one                                                                     | `{}`             |
| `cluster.worker.common.customStartupProbe`                                | Custom startupProbe that overrides the default one                                                                       | `{}`             |
| `cluster.worker.common.resources.limits`                                  | The resources limits for the Ray Cluster Worker (common) containers                                                      | `{}`             |
| `cluster.worker.common.resources.requests`                                | The requested resources for the Ray Cluster Worker (common) containers                                                   | `{}`             |
| `cluster.worker.common.podSecurityContext.enabled`                        | Enabled Ray Cluster Worker (common) pods' Security Context                                                               | `true`           |
| `cluster.worker.common.podSecurityContext.fsGroup`                        | Set Ray Cluster Worker (common) pod's Security Context fsGroup                                                           | `1001`           |
| `cluster.worker.common.containerSecurityContext.enabled`                  | Enabled containers' Security Context                                                                                     | `true`           |
| `cluster.worker.common.containerSecurityContext.runAsUser`                | Set containers' Security Context runAsUser                                                                               | `1001`           |
| `cluster.worker.common.containerSecurityContext.runAsNonRoot`             | Set container's Security Context runAsNonRoot                                                                            | `true`           |
| `cluster.worker.common.containerSecurityContext.privileged`               | Set container's Security Context privileged                                                                              | `false`          |
| `cluster.worker.common.containerSecurityContext.readOnlyRootFilesystem`   | Set container's Security Context readOnlyRootFilesystem                                                                  | `true`           |
| `cluster.worker.common.containerSecurityContext.allowPrivilegeEscalation` | Set container's Security Context allowPrivilegeEscalation                                                                | `false`          |
| `cluster.worker.common.containerSecurityContext.capabilities.drop`        | List of capabilities to be dropped                                                                                       | `["ALL"]`        |
| `cluster.worker.common.containerSecurityContext.seccompProfile.type`      | Set container's Security Context seccomp profile                                                                         | `RuntimeDefault` |
| `cluster.worker.common.command`                                           | Override default container command (useful when using custom images)                                                     | `[]`             |
| `cluster.worker.common.args`                                              | Override default container args (useful when using custom images)                                                        | `[]`             |
| `cluster.worker.common.hostAliases`                                       | Ray Cluster Worker (common) pods host aliases                                                                            | `[]`             |
| `cluster.worker.common.podLabels`                                         | Extra labels for Ray Cluster Worker (common) pods                                                                        | `{}`             |
| `cluster.worker.common.podAnnotations`                                    | Annotations for Ray Cluster Worker (common) pods                                                                         | `{}`             |
| `cluster.worker.common.podAffinityPreset`                                 | Pod affinity preset. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                               | `""`             |
| `cluster.worker.common.podAntiAffinityPreset`                             | Pod anti-affinity preset. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                          | `soft`           |
| `cluster.worker.common.nodeAffinityPreset.type`                           | Node affinity preset type. Ignored if `server.affinity` is set. Allowed values: `soft` or `hard`                         | `""`             |
| `cluster.worker.common.nodeAffinityPreset.key`                            | Node label key to match. Ignored if `server.affinity` is set                                                             | `""`             |
| `cluster.worker.common.nodeAffinityPreset.values`                         | Node label values to match. Ignored if `server.affinity` is set                                                          | `[]`             |
| `cluster.worker.common.affinity`                                          | Affinity for Ray Cluster Worker (common) pods assignment                                                                 | `{}`             |
| `cluster.worker.common.nodeSelector`                                      | Node labels for Ray Cluster Worker (common) pods assignment                                                              | `{}`             |
| `cluster.worker.common.tolerations`                                       | Tolerations for Ray Cluster Worker (common) pods assignment                                                              | `[]`             |
| `cluster.worker.common.priorityClassName`                                 | Ray Cluster Worker (common) pods' priorityClassName                                                                      | `""`             |
| `cluster.worker.common.topologySpreadConstraints`                         | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template | `[]`             |
| `cluster.worker.common.schedulerName`                                     | Name of the k8s scheduler (other than default) for Ray Cluster Worker (common) pods                                      | `""`             |
| `cluster.worker.common.terminationGracePeriodSeconds`                     | Seconds Redmine pod needs to terminate gracefully                                                                        | `""`             |
| `cluster.worker.common.lifecycleHooks`                                    | for the Ray Cluster Worker (common) container(s) to automate configuration before or after startup                       | `{}`             |
| `cluster.worker.common.extraEnvVars`                                      | Array with extra environment variables to add to Ray Cluster Worker (common) nodes                                       | `[]`             |
| `cluster.worker.common.extraEnvVarsCM`                                    | Name of existing ConfigMap containing extra env vars for Ray Cluster Worker (common) nodes                               | `""`             |
| `cluster.worker.common.extraEnvVarsSecret`                                | Name of existing Secret containing extra env vars for Ray Cluster Worker (common) nodes                                  | `""`             |
| `cluster.worker.common.extraVolumes`                                      | Optionally specify extra list of additional volumes for the Ray Cluster Worker (common) pod(s)                           | `[]`             |
| `cluster.worker.common.extraVolumeMounts`                                 | Optionally specify extra list of additional volumeMounts for the Ray Cluster Worker (common) container(s)                | `[]`             |
| `cluster.worker.common.sidecars`                                          | Add additional sidecar containers to the Ray Cluster Worker (common) pod(s)                                              | `[]`             |
| `cluster.worker.common.initContainers`                                    | Add additional init containers to the Ray Cluster Worker (common) pod(s)                                                 | `[]`             |
| `cluster.worker.groupSpecs`                                               | Set worker groupspec parameters                                                                                          | `[]`             |
| `cluster.serviceAccount.create`                                           | Specifies whether a ServiceAccount should be created                                                                     | `true`           |
| `cluster.serviceAccount.name`                                             | The name of the ServiceAccount to use.                                                                                   | `""`             |
| `cluster.serviceAccount.annotations`                                      | Additional Service Account annotations (evaluated as a template)                                                         | `{}`             |
| `cluster.serviceAccount.automountServiceAccountToken`                     | Automount service account token for the server service account                                                           | `false`          |

The above parameters map to the env variables defined in [bitnami/kuberay](https://github.com/bitnami/containers/tree/main/bitnami/kuberay). For more information please refer to the [bitnami/kuberay](https://github.com/bitnami/containers/tree/main/bitnami/kuberay) image documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install my-release \
  --set apiserver.enabled=true \
    REGISTRY_NAME/REPOSITORY_NAME/kuberay
```

The above command enables the KubeRay API Server.

> NOTE: Once this chart is deployed, it is not possible to change the application's access credentials, such as usernames or passwords, using Helm. To change these application credentials after deployment, delete any persistent volumes (PVs) used by the chart and re-deploy it, or use the application's built-in administrative tools if available.

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install my-release -f values.yaml REGISTRY_NAME/REPOSITORY_NAME/kuberay
```

> Note: You need to substitute the placeholders `REGISTRY_NAME` and `REPOSITORY_NAME` with a reference to your Helm chart registry and repository. For example, in the case of Bitnami, you need to use `REGISTRY_NAME=registry-1.docker.io` and `REPOSITORY_NAME=bitnamicharts`.
> **Tip**: You can use the default [values.yaml](https://github.com/bitnami/charts/tree/main/bitnami/kuberay/values.yaml)

## Configuration and installation details

### [Rolling VS Immutable tags](https://docs.bitnami.com/tutorials/understand-rolling-tags-containers)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

### Additional environment variables

In case you want to add extra environment variables (useful for advanced operations like custom init scripts), you can use the `extraEnvVars` property inside the `operator`, `apiserver` and `cluster` sections.

```yaml
operator:
  extraEnvVars:
    - name: LOG_LEVEL
      value: error
```

Alternatively, you can use a ConfigMap or a Secret with the environment variables. To do so, use the `extraEnvVarsCM` or the `extraEnvVarsSecret` values inside the `operator`, `apiserver` and `cluster` sections.

### Sidecars

If additional containers are needed in the same pod as kuberay (such as additional metrics or logging exporters), they can be defined using the `sidecars` parameter inside the `operator`, `apiserver` and `cluster` sections. If these sidecars export extra ports, extra port definitions can be added using the `service.extraPorts` parameter. [Learn more about configuring and using sidecar containers](https://docs.bitnami.com/kubernetes/apps/kuberay/administration/configure-use-sidecars/).

If additional containers are needed in the same pod as kuberay (such as additional metrics or logging exporters), they can be defined using the `sidecars` parameter inside the `operator`, `apiserver` and `cluster` sections. If these sidecars export extra ports, extra port definitions can be added using the `service.extraPorts` parameter. [Learn more about configuring and using sidecar containers](https://docs.bitnami.com/kubernetes/apps/kuberay/administration/configure-use-sidecars/).

### Deploying Ray Cluster

The Bitnami KubeRay chart allows deploying a RayCluster object. It is possible to define the head parameters under the `cluster.head` section, as well as the properties of the workers using the `cluster.worker` section. It is possible to describe different groupspecs under the `cluster.worker.groupSpecs` section (any parameter not defined will be taken from the `cluster.worker.common` section).

### Pod affinity

This chart allows you to set your custom affinity using the `affinity` parameter. Find more information about Pod affinity in the [kubernetes documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity).

As an alternative, use one of the preset configurations for pod affinity, pod anti-affinity, and node affinity available at the [bitnami/common](https://github.com/bitnami/charts/tree/main/bitnami/common#affinities) chart. To do so, set the `podAffinityPreset`, `podAntiAffinityPreset`, or `nodeAffinityPreset` parameters inside the `operator`, `apiserver` and `cluster` sections.

## Troubleshooting

Find more information about how to deal with common errors related to Bitnami's Helm charts in [this troubleshooting guide](https://docs.bitnami.com/general/how-to/troubleshoot-helm-chart-issues).

## License

Copyright &copy; 2024 Broadcom. The term "Broadcom" refers to Broadcom Inc. and/or its subsidiaries.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

<http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.