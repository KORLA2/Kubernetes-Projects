
Through AWS we already have users so  it is easy to set RBAC to EKS cluster.

One who creates cluster is admin.

When EKS cluster was running successfully there is a  ```aws-auth``` config map in kube-system namespace. 

When we want to give a AWS user certain permissions on EKS cluster  this aws-auth is used to map kubernetes user to AWS User.

When cluster is ready it generates system:masters group which has all admin permissions by attaching AWS user to this group can have admin permssions..

There is a clusterrole called admin by attaching this role to user can have admin permissions.

