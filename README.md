
Kubernetes operator to deploy and manage RabbitMQ clusters.

Homepage: https://www.rabbitmq.com/kubernetes/operator/operator-overview.html

## Quickstart

```
$ helm install -g --wait --create-namespace -n rabbitmq-operator ./chart
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| replicaCount | int | `1` | Number of replicas (pods) to launch. |
| crd.create | bool | `true` | To create the crd for installation | 
|imageCredentials.registry | string | `""` | If the docker registry is private |
| imageCredentials.username | string | `""` | Username registry |
| imageCredentials.password | string | `""` | Password for registry |
| imageCredentials.email | string | `""` | email for registry |
| image.repository | string | `"rabbitmqoperator/cluster-operator"` | Name of the image repository to pull the container image from. |
| image.pullPolicy | string | `"IfNotPresent"` | [Image pull policy](https://kubernetes.io/docs/concepts/containers/images/#updating-images) for updating already existing images on a node. |
| image.tag | string | `"1.8.1"` | Image tag override for the default value (chart appVersion). |
| imagePullSecrets | list | `[]` | Reference to one or more secrets to be used when [pulling images](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/#create-a-pod-that-uses-your-secret) (from private registries). |
| nameOverride | string | `""` | A name in place of the chart name for `app:` labels. |
| fullnameOverride | string | `""` | A name to substitute for the full names of resources. |
| serviceAccount.create | bool | `true` | Enable service account creation. |
| serviceAccount.annotations | object | `{}` | Annotations to be added to the service account. |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template. |
| rbac.create | bool | `true` | Enable the creation of RBAC resources. If disabled, the operator (ie. the person installing the chart) is responsible for creating the necessary resources based on the templates. |
| podAnnotations | object | `{}` | Annotations to be added to pods. |
| priorityClassName | string | `""` | Specify a priority class name to set [pod priority](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/#pod-priority). |
| podSecurityContext | object | `{}` | Pod [security context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-pod). See the [API reference](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#security-context) for details. |
| securityContext | object | `{}` | Container [security context](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/#set-the-security-context-for-a-container). See the [API reference](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#security-context-1) for details. |
| podMonitor.enabled | bool | `false` | Enable Prometheus PodMonitor to monitor the operator. |
| podMonitor.interval | string | `"30s"` | Interval at which metrics should be scraped. |
| resources | object | No requests or limits. | Container resource [requests and limits](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/). See the [API reference](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#resources) for details. |
| nodeSelector | object | `{}` | [Node selector](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector) configuration. |
| tolerations | list | `[]` | [Tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) for node taints. See the [API reference](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#scheduling) for details. |
| affinity | object | `{}` | [Affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) configuration. See the [API reference](https://kubernetes.io/docs/reference/kubernetes-api/workload-resources/pod-v1/#scheduling) for details. |
| annotation | object | `{}` | [Annotations](https://kubernetes.io/docs/concepts/overview/working-with-objects/annotations/) 
| rabbitmq.serviceMonitor.enabled | bool | `false` | Enable Prometheus ServiceMonitor to monitor RabbitMQ clusters created by the operator. |
| rabbitmq.serviceMonitor.interval | string | `"30s"` | Interval at which metrics should be scraped. |


## Examples

In addition, a number of [examples](https://github.com/rabbitmq/cluster-operator/tree/main/docs/examples) can be found in official repository.
## Development

## Update operator

```
go get -u github.com/brendanjryan/k8split
```

```
VERSION="1.8.1"

mkdir tmp

curl -L "https://github.com/rabbitmq/cluster-operator/releases/download/v${VERSION}/cluster-operator.yml" > tmp/cluster-operator.yaml
```

MacOs

```
~/go/bin/k8split -o tmp tmp/cluster-operator.yaml
```
