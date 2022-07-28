# Gitlab runners autoscaling AWS Cloudformation template

AWS CloudFormation template that deploys a GitLab runner with docker-machine executor into AWS environment. This setup allows one to autoscale AWS instances depends on the workload and working hours.

Based on [aws-autoscaling-gitlab-runner](https://github.com/chialab/aws-autoscaling-gitlab-runner). Key differences:
* AMI 2 Linux
* Systemd instead of Sysvinit
* SSM login instead of SSH
* Gitlab docker-machine
* Gitlab live debug enabled
* Cloudwatch agent
* It works.

## VPC

Template integrated with [widdix](https://github.com/widdix/aws-cf-templates/tree/master/vpc) Cloudformation templates. You will need to create VPC first and pass VPC stack name in the parameters.

## SSM login

Gitlab manager instance does not use ssh keys for incoming connections. Run `ssm start-session` instead.

## Gitlab live debug

Gitlab manager security group allows connections to 8093 tcp port from gitlab.com subnets. It was done to enable Gitlab live debug.

## Security

Due to nature of docker-machine this stack should be deployed in its own environment. Consider using AWS landing zone and separated AWS account for Gitlab runners.