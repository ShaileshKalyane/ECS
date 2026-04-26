# ECS Fargate - Node Server Deployment

Terraform configuration to deploy `andalike/node-server-8080-1` on AWS ECS Fargate with an Application Load Balancer.

## Architecture

- **VPC** with 2 public subnets across 2 AZs
- **ECS Fargate** cluster running the container on port 8080
- **Application Load Balancer** accepting traffic on port 80 and forwarding to port 8080
- **CloudWatch Logs** with 7-day retention

## Prerequisites

- [Terraform](https://developer.hashicorp.com/terraform/install) >= 1.0
- AWS CLI configured with profile `edii-ai-bot-1`

## Usage

```bash
# Initialize
terraform init

# Preview changes
terraform plan

# Deploy
terraform apply

# Destroy
terraform destroy
```

## Configuration

| Setting | Value |
|---|---|
| AWS Profile | `edii-ai-bot-1` |
| Region | `us-east-1` |
| Image | `andalike/node-server-8080-1` |
| Container Port | 8080 |
| ALB Port | 80 |
| CPU | 256 (0.25 vCPU) |
| Memory | 512 MB |
| Desired Count | 1 |

## Output

After `terraform apply`, the ALB DNS name is printed:

```
alb_dns_name = "ecs-alb-XXXXXXXXXX.us-east-1.elb.amazonaws.com"
```

Hit it on port 80 to reach the service:

```bash
curl http://<alb_dns_name>
```
