# NonameSec Installation

This details installation and daily operations of the nonamesec product on the GISCS environment. 



```
mermaid
graph TD
    client[Client] -->|1. Request| loadBalancer{Load Balancer}
    loadBalancer -->|2. Distribute| webServer1[Web Server 1]
    loadBalancer -->|2. Distribute| webServer2[Web Server 2]
    loadBalancer -->|2. Distribute| webServer3[Web Server 3]

    webServer1 -->|3. Process| appServer1[Application Server 1]
    webServer2 -->|3. Process| appServer2[Application Server 2]
    webServer3 -->|3. Process| appServer3[Application Server 3]

    appServer1 -->|4. Request Data| database[Database]
    appServer2 -->|4. Request Data| database
    appServer3 -->|4. Request Data| database

    database -->|5. Return Data| appServer1
    database -->|5. Return Data| appServer2
    database -->|5. Return Data| appServer3

    appServer1 -->|6. Response| webServer1
    appServer2 -->|6. Response| webServer2
    appServer3 -->|6. Response| webServer3

    webServer1 -->|7. Deliver| client
    webServer2 -->|7. Deliver| client
    webServer3 -->|7. Deliver| client

    classDef layer fill:#f9f,stroke:#333,stroke-width:2px;
    class client,webServer1,webServer2,webServer3 layer;
    class appServer1,appServer2,appServer3 layer;
    class database layer;

```
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








Typical output of successful completion will have similar output as shown below

```
2024-01-12 13:32:15 [ℹ]  waiting for CloudFormation stack "eksctl-nonamesec-nodegroup-noname-engines"
2024-01-12 13:33:23 [ℹ]  waiting for CloudFormation stack "eksctl-nonamesec-nodegroup-noname-engines"
2024-01-12 13:33:23 [ℹ]  waiting for the control plane to become ready
2024-01-12 13:33:25 [✔]  saved kubeconfig as "C:\\cygwin64\\home\\gko8774\\.kube\\config"
2024-01-12 13:33:25 [ℹ]  no tasks
2024-01-12 13:33:25 [✔]  all EKS cluster resources for "nonamesec" have been created
2024-01-12 13:33:26 [ℹ]  nodegroup "noname-engines" has 0 node(s)
2024-01-12 13:33:26 [ℹ]  waiting for at least 1 node(s) to become ready in "noname-engines"
2024-01-12 13:33:42 [ℹ]  nodegroup "noname-engines" has 1 node(s)
2024-01-12 13:33:42 [ℹ]  node "ip-172-31-21-117.us-west-1.compute.internal" is ready
2024-01-12 13:33:43 [ℹ]  creating addon
2024-01-12 13:34:32 [ℹ]  addon "coredns" active
2024-01-12 13:34:33 [ℹ]  creating addon
2024-01-12 13:35:13 [ℹ]  addon "kube-proxy" active
2024-01-12 13:35:16 [ℹ]  kubectl command should work with "C:\\cygwin64\\home\\gko8774\\.kube\\config", try 'kubectl get nodes'
2024-01-12 13:35:16 [✔]  EKS cluster "nonamesec" in "us-west-1" region is ready

```
Alternatively you can monitor your AWS CloudFormation  stack for events related to the cluster creation

2. Then create .github folder and then create workflow folder inside .github folder 
3. create file with .yml extension and write the workflow code
4. Create a github repository 
5. Create secrets in github repo
        Go to settings of repo
        click on secrets and variables
6. Test communication to the nonamesec UI using a web browser

