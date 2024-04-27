## How does a pod to pod communication work ?

Using the pod IP one pod can communicate with other pod . In general pod has the DNS resolution 

`podIP.namepsace.pod.cluster-domain.example`

For example if the other pod is in default namespace and it's IP is 192.0.0.8  and domain name of cluster is cluster.local then pod has following DNS name:

`192.0.0.8.default.pod.cluster.local`

