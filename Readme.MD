# Sample EKS word-press deployment using EKS

## Steps 
1. Create EC2 instance for deployment - ubuntu prefered.
2. Create EC2 iam role and attach aws admin policy to it.
3. Add EC2 iam role to EC2 instance.
2. Download eksctl using command.
    `curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp`
    `sudo mv /tmp/eksctl /usr/local/bin`
3. check the version
    `eksctl version`
4. Install kubectl - https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
5. clone repo to EC2 instance
6. Create cluster with eksctl - `eksctl create cluster -f eks-wordpress.yaml`

## eksctl yaml
1. You can find config for yaml here https://eksctl.io/usage/schema/

