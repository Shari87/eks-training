# I. Authenticate Terraform to AWS

## 1. First of all, create an AWS user with high privileges

https://console.aws.amazon.com/console/home

## 2. Then, Install AWS CLI locally & Configure this user locally with AWS CLI

Check [docker-compose.yaml](docker-compose.yaml)

```sh
docker-compose run --rm aws configure --profile terraform-operator
```

## 3. Configure Terraform to use the AWS user with the AWS provider

Check [docker-compose.yaml](docker-compose.yaml)


## 4. Run Terraform Example to validate the authentication & authorization to AWS

Check [main.tf](main.tf)

then : 

```sh
docker-compose run --rm terraform init
docker-compose run --rm terraform apply
```


# II. Authenticate kubectl to the Cluster

## 1. Create IAM Policy for EKS admin access
https://console.aws.amazon.com/console/home

## 2. Create AWS User (kubectl-operator)
https://console.aws.amazon.com/console/home

## 3. Grant "kubectl-operator" cluster-admin access thru Terraform
[main.tf](main.tf) : add to user to `system:masters` k8s group
More https://kubernetes.io/docs/reference/access-authn-authz/rbac/

## 4. Configure local profile for "kubectl-operator"
`aws configure --profile kubectl-operator`

## 3. Install/configure "kubectl" & "aws-iam-authenticator"
  - Install `kubectl` CLI
  - `aws-iam-authenticator` CLI (image: `abdennour/kubectl:v1.14.7-aws1.16.277`)
  - `AWS_PROFILE` envvar are visible by `kubectl`
  - `KUBECONFIG` envvar is visible by `kubectl`

## II. Verify Settings:

`docker-compose run --rm kubectl get nodes`
