## Setting Up Ingress on EKS

To monitor ingress rules we need ingress cotroller. AWS has its own ingress controller called Loadbalancercontroller. Loadbalancercontroller pod in the kubernetes cluster needs 
some permissions to access AWS resources. BY attaching IAM roles and attach these roles to service account  through role binding . If  Loadbalancer controller has permissions to 
access AWS resources it can launch services that are present in ingress resource.

![image](https://github.com/KORLA2/Kubernetes-Projects/assets/96729391/d82398a2-8fec-4122-b11e-dde813bfc4f7)
