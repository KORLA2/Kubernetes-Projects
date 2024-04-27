## How does a pod to pod communication work ?

Using the pod IP one pod can communicate with other pod . In general pod has the DNS resolution 

`podIP.namepsace.pod.cluster-domain.example`

For example if the other pod is in default namespace and it's IP is 192.0.0.8  and domain name of cluster is cluster.local then pod has following DNS name:

`192.0.0.8.default.pod.cluster.local`

```But pod IP cannot be used as pods are ephemeral and we can't even use pod name as pod name cannot be resolved to it's IP  ```

So to communicate with pod we need services

## How does name of the service is resolved to IP?

In every pod under /etc/resolv.conf there is a list of all static IPS  

![image](https://github.com/KORLA2/Kubernetes-Projects/assets/96729391/fedc7025-0e89-49a9-bd10-7eb868d5a6cc)

When service name was used the request goes to kube-dns service and then forwards to core-dns pod in kube-system namespace which is responsible for dns resolution.

So we can use service name to communicate with other pod but not pod name.
