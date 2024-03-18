# Setting up EKS cluster manually.

AWS manages masternodes. 

Scales , backsup the master nodes , installs the necessary processes like API server, controller manager , etcd, scheduler.

EKS properly secures the kubernetes. Integrated with many AWS services .

1. Before starting with , as cluster was managed by AWS as it needs to access other resources we have to assign a IAM role to cluster.
   
