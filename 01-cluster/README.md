# Getting started with Amazon EKS – `eksctl`<a name="getting-started-eksctl"></a>

You can create a cluster with one of the following node types\. To learn more about each type, see [Amazon EKS nodes](https://docs.aws.amazon.com/eks/latest/userguide/eks-compute.html)\. After your cluster is deployed, you can add other node types\.
+ **Fargate – Linux** – Select this type of node if you want to run Linux applications on AWS Fargate\.
+ **Managed nodes – Linux** – Select this type of node if you want to run Amazon Linux applications on Amazon EC2 instances\.

We are going to use Fargate – Linux with existing VPC for our demo.

# Creating and managing clusters

## Creating a cluster

**To create your cluster with Fargate Linux nodes**

Create your Amazon EKS cluster with an [AWS Fargate profile](https://docs.aws.amazon.com/eks/latest/userguide/fargate-profile.html) and [Pod execution role](https://docs.aws.amazon.com/eks/latest/userguide/pod-execution-role.html) with the following command\. Replace `my-cluster` with your own value\. Though you can create a cluster in any [Amazon EKS supported Region](https://docs.aws.amazon.com/general/latest/gr/eks.html), in this tutorial, it's created in **US West \(Oregon\) us\-west\-2**\.

   ```
   eksctl create cluster \
   --name my-cluster \
   --region us-west-2 \
   --fargate
   ```

   The previous command creates a cluster and Fargate profile using primarily default settings\. After creation is complete, view the stack named `eksctl-my-cluster-cluster` in the AWS CloudFormation console to review all resources that were created\. For a list of all settings and options, enter `eksctl create cluster -h`\. For documentation of all settings and options, see [Creating and Managing Clusters](https://eksctl.io/usage/creating-and-managing-clusters/) in the `eksctl` documentation\.

   **Output**

   You'll see several lines of output as the cluster and Fargate profile are created\. Creation takes several minutes\. The last line of output is similar to the following example line\.

   ```
   ...
   [✓]  EKS cluster "my-cluster" in "us-west-2" region is ready
   ```

   If nodes fail to join the cluster, then see [Nodes fail to join cluster](https://docs.aws.amazon.com/eks/latest/userguide/troubleshooting.html#worker-node-fail) in the Troubleshooting guide\.

   `eksctl` created a `kubectl` `config` file in `~/.kube` or added the new cluster's configuration within an existing `config` file in `~/.kube`\.

## Using Config Files

You can create a cluster using a config file instead of flags.

First, create `cluster.yaml` file: 

If you needed to use an existing VPC, you can use a config file like this:

```yaml
apiVersion: eksctl.io/v1alpha5
kind: ClusterConfig

metadata:
  name: cluster-in-existing-vpc
  region: eu-north-1

vpc:
  subnets:
    private:
      eu-north-1a:  id: subnet-0ff156e0c4a6d300c 
      eu-north-1b:  id: subnet-0549cdab573695c03 
      eu-north-1c:  id: subnet-0426fb4a607393184 

iam:
  serviceRoleARN: "EKS Role ARN"

cloudWatch:
  clusterLogging:
    enableTypes:
      - audit
      - authenticator
      - api
      - controllerManager
      - scheduler

fargateProfiles:
  - name: fp-default
    selectors:
      - namespace: default
      - namespace: kube-system
    subnets:
      - subnet-1234567890 # Private subnet 
``` 

Next, run this command:

```
eksctl create cluster -f cluster.yaml
```
eksctl created a kubectl config file in ~/.kube or added the new cluster's configuration within an existing config file in ~/.kube.

To delete this cluster, run:

```
eksctl delete cluster -f cluster.yaml
```