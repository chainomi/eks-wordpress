# Sample EKS word-press deployment using EKS
This is a simple word press kubernetes deployment using AWS EKS. The Word press application uses a mysql database (not externally exposed)

## Setup
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
8. Clone repo to EC2 instance
9. cd into cloned repo and create cluster with eksctl - `eksctl create cluster -f eks-wordpress.yaml`
10. Cluster creation will take 15-20 minutes. This process uses cloudformation in the backgroud
11. Run `kubectl get nodes` to see all nodes created

## Deployment
1. Deploy configMap - `kubectl create -f configmap.yaml`
2. Deploy mysql - `kubectl create -f mysql-deployment.yaml`
3. Deploy wordpress - `kubectl create -f wordpress-deployment.yaml`
4. Run `kubectl get all` to see confimap, services, deployments and pods
5. Perform an nslookup on the load balancer to check for availiability - `nslookup <load_balancer_domain_name>
6. Keep trying until domain name has propergated and can be resolved
7. Open the load balancer url in a browser to view the word press application


## eksctl yaml
1. You can find config for yaml here https://eksctl.io/usage/schema/

