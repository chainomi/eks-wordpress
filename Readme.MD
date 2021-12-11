# Sample EKS word-press deployment using EKS
This is a simple word press kubernetes deployment using AWS EKS. The Word press application uses a mysql database (not externally exposed)

## Setting up instance and tools
1. Create EC2 instance for deployment - ubuntu prefered.
2. Create EC2 iam role and attach aws admin policy to it.
3. Add EC2 iam role to EC2 instance.
4. Install aws iam authenticator. Need this to give kubectl access to the eks cluster - https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html
5. Download eksctl using command.
    `curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp`
    `sudo mv /tmp/eksctl /usr/local/bin`
6. check the version
    `eksctl version`
7. Install kubectl - https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

## Setting up EKS cluster and resources
1. Clone repo to EC2 instance.
2. cd into cloned repo and create cluster with eksctl - `eksctl create cluster -f eks-wordpress.yaml`
3. Cluster creation will take 15-20 minutes. Note that this process uses cloudformation in the backgroud. Cloud formation stack can be viewed from AWS console.
4. Run `kubectl get nodes` to see all nodes created.

## Deployment
1. Deploy configMap - `kubectl create -f configmap.yaml`
2. Deploy mysql - `kubectl create -f mysql-deployment.yaml`
3. Deploy wordpress - `kubectl create -f wordpress-deployment.yaml`
4. Run `kubectl get all` to see confimap, services, deployments and pods
5. Perform an nslookup on the load balancer to check for availiability - `nslookup <load_balancer_domain_name>
6. Keep trying until domain name has propergated and can be resolved
7. Open the load balancer url in a browser to view the word press application

## Deleting deployment & EKS cluster
1. Delete configMap - `kubectl create -f configmap.yaml`
2. Delete mysql - `kubectl create -f mysql-deployment.yaml`
3. Delete wordpress - `kubectl create -f wordpress-deployment.yaml`
4. Delete eks cluser - `eksctl delete cluster -f eks-wordpress.yaml`

## eksctl yaml
1. This is a good resource for creating eksctl yaml files - https://eksctl.io/usage/schema/
