# Setting up EKS cluster manually.

AWS manages masternodes. 

Scales , backsup the master nodes , installs the necessary processes like API server, controller manager , etcd, scheduler.

# Deploying Cluster with AWS Cli

1. Create Role to EKS cluster so that kubernetes masternodes can access other AWS services.

   ``` aws iam create-role --role-name=master-node-role -assume-role-policy-document file://assume-policy.json ```

### Note the role-arn

   <b>assume-policy.json</b>
   
   ```
 {
    "Version": "2012-10-17",
    "Statement": [
    {
    
       "Effect": "Allow",
        "Principal": {
          "Service": "eks.amazonaws.com"
        },
        "Action": "sts:AssumeRole"
      }
    ]
}
```

  ```aws  iam attach-role-policy --role-name master-node-role --policy-arn arn:aws:iam::aws:policy/AmazonEKSClusterPolicy
  ```

2.  Create eks cluster

```
  aws eks create-cluster \
--name my-eks-cluster \
--role-arn $role_arn \
--region ap-south-1\
--resources-vpc-config subnetIds=subnet-063efe1fa0c5d4913,subnet-06f91e563755e2077,subnet-0824d16f8536b3681,securityGroupIds=sg-0960d3a116ba912e1,endpointPublicAccess=true,endpointPrivateAccess=false

 ```
3. Update Kube config
   
   ``` aws eks update-kube-config --name=my-eks-cluster --region ap-south-1  ```

3. Now create Role for worker nodes

  ``` aws iam create-role --role-name worker-node-role --assume-role-policy-document file://assume-node-policy.json ```

  Note the role arn
  
`assume-node-policy.json`

```
{
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Principal": {
          "Service": "ec2.amazonaws.com"
        },
        "Action": "sts:AssumeRole"
      }
    ]
}
```
```
aws iam attach-role-policy --role-name worker-node-role --policy-arn arn:aws:iam::aws:policy/AmazonEKSWorkerNodePolicy
aws iam attach-role-policy --role-name worker-node-role --policy-arn arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy
aws iam attach-role-policy --role-name worker-node-role --policy-arn arn:aws:iam::aws:policy/AmazonEC2ContainerRegistryReadOnly
```

4. Create worker nodes

 ```
     
     aws eks create-nodegroup \
--cluster-name my-eks-cluster \
--nodegroup-name my-node-group \
--node-role $role_arn \
--subnets subnet-0ec47e6ae964a233f \
--disk-size 200 \
--scaling-config minSize=1,maxSize=2,desiredSize=1 \
--instance-types t2.small

 ```


  
  

   


    
   
