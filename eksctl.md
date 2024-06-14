eksctl simplifies the process of creating the EKS cluster.

# Create Cluster
```
eksctl create cluster --name=eksdemo1 \
                      --region=us-east-1 \
                      --zones=us-east-1a,us-east-1b \
                      --without-nodegroup 
```
# Create Node group
- These add-ons will create the respective IAM policies for us automatically within our Node Group role.
```
eksctl create nodegroup --cluster=eksdemo1 \
                       --region=us-east-1 \
                       --name=eksdemo1-ng-public1 \
                       --node-type=t3.medium \
                       --nodes=2 \
                       --nodes-min=2 \
                       --nodes-max=4 \
                       --node-volume-size=20 \
                       --ssh-access \
                       --ssh-public-key=kube-demo \
                       --managed \
                       --asg-access \
                       --external-dns-access \
                       --full-ecr-access \
                       --appmesh-access \
                       --alb-ingress-access 
```

                       
```
 Create SSH key for Node access (if you need it)
yum install openssh
mkdir -p ~/.ssh/
PASSPHRASE="mysuperstrongpassword"
ssh-keygen -t rsa -b 4096 -N "${PASSPHRASE}" -C "your_email@example.com" -q -f  ~/.ssh/id_rsa
chmod 400 ~/.ssh/id_rsa*


eksctl create cluster --name getting-started-eks \
--region ap-southeast-2 \
--version 1.16 \
--managed \
--node-type t2.small \
--nodes 1 \
--node-volume-size 200 \
--ssh-access \
--ssh-public-key=~/.ssh/id_rsa.pub \

```
