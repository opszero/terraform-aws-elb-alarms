# AWS ELB Cloudwatch

This Terraform module manages CloudWatch Alarms for an ALB in the region. It does NOT create or manage Load Balancers, only Metric Alarms.

**Requires**:

- AWS Provider
- Terraform 0.12

## Alarms Created

Alarms Always Created:

- Any 5xx errors from the target group
- Any 5xx errors from the load balancer
- Unacceptably high average response times
- Number of unhealthy hosts
- Number of healthy hosts

**Estimated Operating Cost**: $ 0.50 / month

- $ 0.10 / month for Metric Alarms (5x)

## Example

```hcl-terraform
module "aws-alb-alarms" {
  source            = "lorenzoaiello/alb-alarms/aws"
  version           = "x.y.z"
}

```
