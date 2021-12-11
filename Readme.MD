# Sample EKS word-press deployment using EKS

## Steps 
1. Create EC2 instance for deployment - ubuntu prefered
2. Download Kubectl using command 
    `curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp`
    `sudo mv /tmp/eksctl /usr/local/bin`
3. check the version
    `eksctl version`
4. Install kubectl - https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/

