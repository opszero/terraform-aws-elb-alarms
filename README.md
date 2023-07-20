<!-- BEGIN_TF_DOCS -->
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
# Pro Support

<a href="https://www.opszero.com"><img src="https://assets.opszero.com/images/opszero_11_29_2016.png" width="300px"/></a>

[opsZero provides support](https://www.opszero.com/devops) for our modules including:

- Email support
- Zoom Calls
- Implementation Guidance
## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_actions_alarm"></a> [actions\_alarm](#input\_actions\_alarm) | A list of actions to take when alarms are triggered. Will likely be an SNS topic for event distribution. | `list(string)` | `[]` | no |
| <a name="input_actions_ok"></a> [actions\_ok](#input\_actions\_ok) | A list of actions to take when alarms are cleared. Will likely be an SNS topic for event distribution. | `list(string)` | `[]` | no |
| <a name="input_evaluation_period"></a> [evaluation\_period](#input\_evaluation\_period) | The evaluation period over which to use when triggering alarms. | `string` | `"5"` | no |
| <a name="input_healthy_hosts_threshold"></a> [healthy\_hosts\_threshold](#input\_healthy\_hosts\_threshold) | The number of healthy hosts. | `string` | `"0"` | no |
| <a name="input_load_balancer_arn"></a> [load\_balancer\_arn](#input\_load\_balancer\_arn) | ELB ARN | `string` | n/a | yes |
| <a name="input_prefix"></a> [prefix](#input\_prefix) | Alarm Name Prefix | `string` | `""` | no |
| <a name="input_response_time_threshold"></a> [response\_time\_threshold](#input\_response\_time\_threshold) | The average number of milliseconds that requests should complete within. | `string` | `"50"` | no |
| <a name="input_statistic_period"></a> [statistic\_period](#input\_statistic\_period) | The number of seconds that make each statistic period. | `string` | `"60"` | no |
| <a name="input_target_group_arn"></a> [target\_group\_arn](#input\_target\_group\_arn) | Target Group ID | `string` | n/a | yes |
| <a name="input_target_group_id"></a> [target\_group\_id](#input\_target\_group\_id) | Target Group ARN | `string` | n/a | yes |
| <a name="input_unhealthy_hosts_threshold"></a> [unhealthy\_hosts\_threshold](#input\_unhealthy\_hosts\_threshold) | The number of unhealthy hosts. | `string` | `"0"` | no |
## Resources

| Name | Type |
|------|------|
| [aws_cloudwatch_metric_alarm.healthy_hosts](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.httpcode_lb_5xx_count](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.httpcode_target_5xx_count](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.target_response_time_average](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.unhealthy_hosts](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
## Outputs

| Name | Description |
|------|-------------|
| <a name="output_alarm_httpcode_lb_5xx_count"></a> [alarm\_httpcode\_lb\_5xx\_count](#output\_alarm\_httpcode\_lb\_5xx\_count) | The CloudWatch Metric Alarm resource block for 5xx errors on the load balancer |
| <a name="output_alarm_httpcode_target_5xx_counts"></a> [alarm\_httpcode\_target\_5xx\_counts](#output\_alarm\_httpcode\_target\_5xx\_counts) | The CloudWatch Metric Alarm resource block for 5xx errors on the target group |
| <a name="output_alarm_target_response_time_average"></a> [alarm\_target\_response\_time\_average](#output\_alarm\_target\_response\_time\_average) | The CloudWatch Metric Alarm resource block for unacceptably high response time averages |
<!-- END_TF_DOCS -->