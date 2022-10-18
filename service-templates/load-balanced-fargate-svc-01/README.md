## Description

This template is compatible with the [shared-fargate-env-01](../../environment-templates/shared-fargate-env-01) template. It creates an ECS service running on a Fargate cluster and relevant ALB Target Group and Listener Rule setup to map to a load balancer provisioned in the environment. 

The service is designed to run in a Private subnet without direct internet access. Service properties like port number, desired task count, task size (cpu/memory units), and docker image URL can be specified through the service input parameters.

The template also provisions a CodePipeline based pipeline to pull application source code before building and deploying it to the Proton service.

For more information see the main [README.md](/README.md).

### Service Inputs

1. port: The backend application port to route traffic to
1. desired_count: The default number of Fargate tasks you want running
1. task_size: The size of the task you want to run
1. image: The name/url of the container image
1. otel_image: The name/url of the AWS OTEL container image. Stick to the default value.
1. backendurl: Service discovery url of the backend service
1. fq_parent_domain: Full FQDN will be <service.name>.<fq_parent_domain>. eg. sample-app-01.demo01.staging.containerofferings.com
1. listener_rule_priority: Application Load Balancer Listener Rule priority, must not collide with existing services."

### Pipeline Inputs

1. service_dir: Source directory for the service
2. dockerfile: The location of the Dockerfile to build
3. unit_test_command: The command to run to unit test the application code

### (Optional) Extend the Service with a Component

The service template which you used above will provision a Fargate service with the infrastructure required for networking, monitoring and scaling the service. In practice you may want to use a template like this for many different purposes and can use components to extend the service template to meet your requirements.