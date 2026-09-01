# Kubernetes API groups
Kubernetes APIs are organized into groups. Some important ones you'll encounter are:


| API version                       | Common resources                                             |
| --------------------------------- | ------------------------------------------------------------ |
| `v1`                              | Pod, Service, ConfigMap, Secret, Namespace                   |
| `apps/v1`                         | Deployment, ReplicaSet, StatefulSet, DaemonSet               |
| `batch/v1`                        | Job, CronJob                                                 |
| `autoscaling/v1`                  | HorizontalPodAutoscaler                                      |
| `autoscaling/v2`                  | HorizontalPodAutoscaler                                      |
| `networking.k8s.io/v1`            | Ingress, NetworkPolicy                                       |
| `policy/v1`                       | PodDisruptionBudget                                          |
| `storage.k8s.io/v1`               | StorageClass, CSIDriver, CSINode                             |
| `rbac.authorization.k8s.io/v1`    | Role, RoleBinding, ClusterRole, ClusterRoleBinding           |
| `scheduling.k8s.io/v1`            | PriorityClass                                                |
| `node.k8s.io/v1`                  | RuntimeClass                                                 |
| `admissionregistration.k8s.io/v1` | ValidatingWebhookConfiguration, MutatingWebhookConfiguration |
| `certificates.k8s.io/v1`          | CertificateSigningRequest                                    |
| `coordination.k8s.io/v1`          | Lease                                                        |
| `discovery.k8s.io/v1`             | EndpointSlice                                                |
| `events.k8s.io/v1`                | Event                                                        |
