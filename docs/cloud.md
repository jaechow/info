# Cloud CLI

The commands you actually use across AWS, GCP, Azure, Kubernetes, and Terraform.

## AWS CLI

### Identity & Auth

Check who you're authenticated as:

```shell
aws sts get-caller-identity
```

List configured profiles:

```shell
aws configure list-profiles
```

Use a specific profile:

```shell
export AWS_PROFILE=production
```

### S3

List buckets:

```shell
aws s3 ls
```

Sync a local directory to S3:

```shell
aws s3 sync ./dist s3://my-bucket/app --delete
```

Download a file:

```shell
aws s3 cp s3://my-bucket/data.json .
```

### CloudWatch Logs

Tail logs in real time:

```shell
aws logs tail /aws/lambda/my-function --follow
```

> Install: `brew install awscli` · `pip install awscli`

---

## Google Cloud (`gcloud`)

### Auth & Config

Login interactively:

```shell
gcloud auth login
```

Set the active project:

```shell
gcloud config set project my-project-id
```

List active configuration:

```shell
gcloud config list
```

### Compute

SSH into a VM:

```shell
gcloud compute ssh my-instance --zone us-central1-a
```

### Cloud Run

Deploy a container:

```shell
gcloud run deploy my-service --source . --region us-central1
```

> Install: `brew install google-cloud-sdk`

---

## Azure (`az`)

Login:

```shell
az login
```

List subscriptions:

```shell
az account list --output table
```

Set active subscription:

```shell
az account set --subscription "My Subscription"
```

> Install: `brew install azure-cli`

---

## kubectl (Kubernetes)

### Context & Namespace

List contexts:

```shell
kubectl config get-contexts
```

Switch context:

```shell
kubectl config use-context production
```

Set default namespace:

```shell
kubectl config set-context --current --namespace=my-app
```

### Pods

List pods:

```shell
kubectl get pods
```

View logs:

```shell
kubectl logs -f deployment/my-app
```

Exec into a pod:

```shell
kubectl exec -it my-pod -- /bin/sh
```

Port-forward a service to localhost:

```shell
kubectl port-forward svc/my-service 8080:80
```

### Quick Debug

Get events sorted by time:

```shell
kubectl get events --sort-by=.lastTimestamp
```

Describe a failing pod:

```shell
kubectl describe pod my-pod
```

> Install: `brew install kubectl` · comes with Docker Desktop

---

## Terraform

### Workflow

Initialize a project:

```shell
terraform init
```

Preview changes:

```shell
terraform plan
```

Apply changes:

```shell
terraform apply
```

Destroy all managed resources:

```shell
terraform destroy
```

!!! warning
    Always run `terraform plan` before `apply` in production environments.

### State

List managed resources:

```shell
terraform state list
```

Show a specific resource:

```shell
terraform state show aws_instance.web
```

> Install: `brew install terraform` · `winget install Hashicorp.Terraform`
