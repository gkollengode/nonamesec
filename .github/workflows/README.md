# NonameSec Installation

This details installation and daily operations of the nonamesec product on the GISCS environment. 


## Installation prerequisites

 - AWS Credentials (AWS_ACCESS_KEY, AWS_SECRET_ACCESS_KEY and AWS_DEFAULT_REGION)
 - eksctl
 - kubectl
 - helm. Follow instructions as detailed [here](https://helm.sh/docs/intro/install/) 
 - kustomize. Instructions for installing is located [here](https://kubectl.docs.kubernetes.io/installation/kustomize/)
 - Github org


## Create the Cluster
Follow these steps

    git clone https://github.com/<ORG-TBD>/<REPO_TBD>/nonanamesec.git
    cd nonamesec/<ENV_TO_DEPLOY>
Edit the ```cluster.yaml``` file to match your AWS environment.

    eksctl create cluster -f cluster.yaml
Wait while the EKS cluster becomes available ( shoud take about 10 - 15 minutes to complete initilalization)


## Destroy the cluster

Enter ```eksctl delete cluster --clustername nonamesec```


## Create files and folders

We use kustomize to set specific values per environment. Folders *environments/[sandbox, pre-prod, prod]* contain specific values for each environment




