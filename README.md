# Amazon EKS using Terraform


## Amazon CLI

We can get the Amazon CLI on [Docker-Hub](https://hub.docker.com/r/amazon/aws-cli) <br/>
We'll need the Amazon CLI to gather information so we can build our Terraform file.

```
# Run Amazon CLI
docker run -it --rm -v ${PWD}:/work -w /work --entrypoint /bin/sh amazon/aws-cli:2.0.43

# some handy tools :)
yum install -y jq gzip nano tar git unzip wget

```

## Login to Amazon

```
# Access your "My Security Credentials" section in your profile. 
# Create an access key

aws configure

Default region name: eu-central-1
Default output format: json
```

# Terraform CLI 

```
# Get Terraform

curl -o /tmp/terraform.zip -LO https://releases.hashicorp.com/terraform/0.13.1/terraform_0.13.1_linux_amd64.zip
unzip /tmp/terraform.zip
chmod +x terraform && mv terraform /usr/local/bin/
terraform
```

## Terraform Amazon Kubernetes Provider 

Documentation on all the Kubernetes fields for terraform [here](https://www.terraform.io/docs/providers/aws/r/eks_cluster.html)

```
cd kubernetes/cloud/amazon/terraform

terraform init

terraform plan
terraform apply

```

# Lets see what we deployed

```
# grab our EKS config
aws eks update-kubeconfig --name getting-started-eks --region eu-central-1

# Get kubectl

curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
chmod +x ./kubectl
mv ./kubectl /usr/local/bin/kubectl

kubectl get nodes
kubectl get deploy
kubectl get pods
kubectl get svc




```

# Output

```
The Terraform will provision the following:

1. Security Groups
2. VPC
3. EKS Cluster and attach it to VPC
4. Spin up the auto scaling group. Attach it to Kubernetes
5. Spin up two pods on deployment using nginX container and service of type load balancer to expose nginX

```

<img width="308" alt="output1" src="https://user-images.githubusercontent.com/44448083/204741844-fb49e0cf-1431-4ea8-adec-af7a33561f37.PNG">


# Clean up 

```
terraform destroy
```
