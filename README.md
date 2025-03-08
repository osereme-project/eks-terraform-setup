 # Terraform Installation And Setup In AWS EC2 Linux Instances
#  Using Terraform to provision a fully managed Amazon EKS Cluster

##### Prerequisite
+ AWS Acccount.
+ Create an ubuntu EC2 Instnace.
+ Create IAM Role With Required Policies.
   + VPCFullAccess
   + EC2FullAcces
   + S3FullAccess  ..etc
   + Administrator Access
+ Attach IAM Role to EC2 Instance.

### CREATE an admin user to manage our EKS Cluster
```sh
sudo adduser eksadmin
sudo echo "eksadmin  ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/eksadmin
sudo su - eksadmin
```
### Install Terraform
### There are several methods to install terraform
### macOS:
``` Package manager
brew tap hashicorp/tap
brew install hashicorp/tap/terraform
```

### Script:
``` sh
$ git clone https://github.com/osereme-project/eks-terraform-setup
$ cd eks-terraform-setup
# install terraform using a bash shell script
$ sh terraform-install.sh

# run the scripts https://github.com/osereme-project/eks-terraform-setup/blob/main/terraform-install.sh
```

# OR install terraform by running the commands below
### Command:
```
$ sudo apt-get update && sudo apt-get install -y gnupg software-properties-common

# Install the HashiCorp GPG key.
$ wget -O- https://apt.releases.hashicorp.com/gpg | \
  gpg --dearmor | \
$ sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null

# Verify the key's fingerprint.
$ gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
 
# The gpg command will report the key fingerprint:
$ /usr/share/keyrings/hashicorp-archive-keyring.gpg
-------------------------------------------------
pub   rsa4096 XXXX-XX-XX [SC]
AAAA AAAA AAAA AAAA
uid           [ unknown] HashiCorp Security (HashiCorp Package Signing) <security+packaging@hashicorp.com>
sub   rsa4096 XXXX-XX-XX [E]

# Download the package information from HashiCorp.
$ sudo apt update

# Install Terraform from the new repository.
$ sudo apt-get install terraform
```

#### Clone terraform scripts
``` sh
$ git clone https://github.com/osereme-project/eks-terraform-setup
$ cd eks-terraform-setup
```

#### <span style="color:orange">Update Your Key Name in variables.tf file before executing terraform script.</span>
## Infrastructure As A Code using Terraform
#### Create Infrastructure(Amazon EKS, IAM Roles, AutoScalingGroups, Launch Configuration, LoadBalancer, NodeGroups,VPC,Subnets,Route Tables,Security Groups, NACLs, ..etc) As A Code Using Terraform Scripts
``` sh
# Initialise to install plugins
$ terraform init 

# Validate terraform scripts
$ terraform validate 

# Plan terraform scripts which will list resources which is going  be created.
$ terraform plan 

# Apply to create resources with 
$ terraform apply --auto-approve
```

```sh
##  Destroy Infrastructure  
$ terraform destroy --auto-approve

## create the kubeconfig file  
$ mkdir .kube/ 
$ vi .kube/config
$ kubectl get pod
$ #!/bin/bash 
$ sh iam-authenticator.sh 
$ kubectl get pod
## deploy cluster auto scaler
$ kubectl apply -f clusterautoscaler.yml

 ```
```
##  Destroy Infrastructure  
```sh
$ terraform destroy --auto-approve 
```


# EKS Getting Started Guide Configuration

This is the full configuration from https://www.terraform.io/docs/providers/aws/guides/eks-getting-started.html

See that guide for additional information.

NOTE: This full configuration utilizes the [Terraform http provider](https://www.terraform.io/docs/providers/http/index.html) to call out to icanhazip.com to determine your local workstation external IP for easily configuring EC2 Security Group access to the Kubernetes servers. Feel free to replace this as necessary.


$ kubectl create deployment autoscaler-demo --image=nginx
$ kubectl get pods --all-namespaces | grep Running | wc -l
$ kubectl get nodes -o yaml | grep pods
$ kubectl scale deployment autoscaler-demo --replicas=20
$ https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html
$ aws-iam-authenticator help
