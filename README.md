# kube-oidc-rbac

A Helm chart used to manage Kubernetes RBAC with OIDC.

## Configuration options

The following table lists the configurable parameters of the kube-oidc-rbac chart and their default values.

| Parameter                                    | Description | Default                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------------------------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `config.bindings`                           |             | [] |
| `config.templates`                           |             | {templates: [{name: admin, rules: [{apiGroups: ['*'], resources: ['*'], verbs: ['*']}]}, {name: editor, rules: [{apiGroups: ['*'], resources: [configmaps, endpoints, persistentvolumeclaims, pods, pods/log, pods/portforward, pods/exec, pods/attach, podtemplates, replicationcontrollers, resourcequotas, secrets, serviceaccounts, services, horizontalpodautoscalers, cronjobs, jobs, events, daemonsets, deployments, deployments/scale, replicasets, ingresses, networkpolicies, poddisruptionbudgets, roles, rolebindings, certificates, statefulsets], verbs: ['*']}]}, {name: viewer, rules: [{apiGroups: ['*'], resources: [configmaps, endpoints, limitranges, persistentvolumeclaims, pods, pods/log, pods/portforward, pods/attach, podtemplates, replicationcontrollers, resourcequotas, services, horizontalpodautoscalers, cronjobs, jobs, events, daemonsets, deployments, replicasets, ingresses, networkpolicies, poddisruptionbudgets], verbs: [get, list, watch, read]}]}, {name: portforward, rules: [{apiGroups: ['*'], resources: [services, pods, pods/portforward], verbs: [get, list]}, {apiGroups: ['*'], resources: [pods/portforward], verbs: [create]}]}, {name: namespace-viewer, rules: [{apiGroups: ['*'], resources: [namespaces], verbs: [get, list, watch]}]}]}{templates: [{name: admin, rules: [{apiGroups: ['*'], resources: ['*'], verbs: ['*']}]}, {name: editor, rules: [{apiGroups: ['*'], resources: [configmaps, endpoints, persistentvolumeclaims, pods, pods/log, pods/portforward, pods/exec, pods/attach, podtemplates, replicationcontrollers, resourcequotas, secrets, serviceaccounts, services, horizontalpodautoscalers, cronjobs, jobs, events, daemonsets, deployments, deployments/scale, replicasets, ingresses, networkpolicies, poddisruptionbudgets, roles, rolebindings, certificates, statefulsets], verbs: ['*']}]}, {name: viewer, rules: [{apiGroups: ['*'], resources: [configmaps, endpoints, limitranges, persistentvolumeclaims, pods, pods/log, pods/portforward, pods/attach, podtemplates, replicationcontrollers, resourcequotas, services, horizontalpodautoscalers, cronjobs, jobs, events, daemonsets, deployments, replicasets, ingresses, networkpolicies, poddisruptionbudgets], verbs: [get, list, watch, read]}]}, {name: portforward, rules: [{apiGroups: ['*'], resources: [services, pods, pods/portforward], verbs: [get, list]}, {apiGroups: ['*'], resources: [pods/portforward], verbs: [create]}]}, {name: namespace-viewer, rules: [{apiGroups: ['*'], resources: [namespaces], verbs: [get, list, watch]}]}] |
| `config.extraTemplates`                           |             | [] |

## Kubeconfig

Using [kubelogin](https://github.com/Azure/kubelogin), in kubeconfig user section, add this:

```
users:
- name: user-oidc
  user:
    exec:
      apiVersion: client.authentication.k8s.io/v1beta1
      args:
      - get-token
      - --oidc-issuer-url=<URL>
      - --oidc-client-id=<CLIENT_ID>
      - --oidc-client-secret=<CLIENT_SECRET>
      - --oidc-extra-scope=email
      command: kubelogin
      env: null
      interactiveMode: IfAvailable
      provideClusterInfo: false
```
