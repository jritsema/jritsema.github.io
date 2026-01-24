---
title: "Projects"
draft: false
summary: "I am passionate about building tools and systems that help developers be more productive and successful. Here is a collection of open-source projects I have created or contributed to over the years, organized by focus area."
---

I am passionate about building tools and systems that help developers be more productive and successful. Here is a collection of open-source projects I have created or contributed to over the years, organized by focus area.

## AI
As AI transforms the technology landscape, I have been building tools to help developers leverage these powerful capabilities:

- **[ECS Express Skill / Kiro Power](https://github.com/jritsema/ecs-express-power/)** - An Agent Skill and Kiro Power to assist with deploying web apps and APIs to AWS using Amazon ECS Express Mode.
- **[AI Agent Accelerator](https://github.com/aws-samples/ai-chat-accelerator)** - Get up and running quickly with an AI agent application on AWS using Bedrock AgentCore and S3 Vectors.
- **[Bedrock AgentCore Memory Explorer](https://github.com/jritsema/agentcore-memory-explorer)** - A modern web UI for exploring and visualizing AWS Bedrock AgentCore memory data. (vibe coded)
- **[MCP CLI](https://github.com/jritsema/mcp-cli)** - MCP CLI is a tool for managing MCP server configuration files. (vibe coded)
- **[AI Chat Accelerator](https://github.com/aws-samples/ai-chat-accelerator)** - A production-ready reference implementation for building RAG-based AI chat applications on AWS.
- **[Bedrock Tools](https://github.com/jritsema/bedrock-tools)** - A streamlined Python library for working with Amazon Bedrock's Conversation API.
- **[AWS News MCP Server](https://github.com/jritsema/aws-news-mcp-server)** - MCP server for AWS news.
- **[AWS News Agent](https://github.com/jritsema/aws-news-agent)** - An AI-powered assistant that helps you stay current with AWS news and announcements.
- **[Page Insights](https://github.com/jritsema/page-insights)** - Leverage AI to generate intelligent summaries of web pages.

## AWS Containers Expertise
I was an early adopter and advocate for AWS Fargate, creating several widely adopted tools that improved the developer experience:

### Fargate Tooling
- **[Fargate Create CLI](https://github.com/turnerlabs/fargate-create)** - A pioneering CLI tool for scaffolding AWS ECS Fargate applications, featuring an opinionated multi-environment setup and an extensive template library.
- **[Fargate CLI](https://github.com/turnerlabs/fargate)** - Simplifies image deployments with support for docker-compose.yml files.
- **[Fargate CLI Build](https://github.com/turnerlabs/fargate-cli-build)** - Build environment for the Fargate CLI.
- **[Terraform Fargate](https://github.com/jritsema/terraform-fargate)** - Simplified, less opinionated version of fargate-create for Fargate deployments.
- **[Fargate SAM](https://github.com/jritsema/fargate-sam)** - Template for deploying public ALB + ECS Fargate services using CloudFormation and SAM CLI.
- **[Fargate SQS Worker](https://github.com/jritsema/sqs-worker)** - Boilerplate for Fargate containers processing SQS queues.

#### Fargate Infrastructure Templates
A collection of production-grade Terraform templates for AWS container deployments (compatible with the Fargate Create CLI tool):
- **[ALB Template](https://github.com/turnerlabs/terraform-ecs-fargate)** - The gold standard for deploying web applications on Fargate, including logging, observability, and auto-scaling.
- **Specialized Templates:**
  - [HTTPS with DNS/TLS](https://github.com/turnerlabs/terraform-ecs-fargate-dns-https)
  - [Network Load Balancer](https://github.com/turnerlabs/terraform-ecs-fargate-nlb)
  - [API Gateway Integration](https://github.com/turnerlabs/terraform-ecs-fargate-apigateway)
  - [Background Workers](https://github.com/turnerlabs/terraform-ecs-fargate-background-worker)
  - [Scheduled Tasks](https://github.com/turnerlabs/terraform-ecs-fargate-scheduled-task)

### Other AWS Container Tools
- **[Ephemeral Preview Environments](https://github.com/aws-samples/ephemeral-preview-containers-furl)** - An innovative solution for container-based preview environments using Lambda.
- **[App Runner Multi-region](https://github.com/aws-samples/apprunner-multiregion)** - Reference architecture for highly resilient, multi-region applications.
- **[App Runner Demo](https://github.com/jritsema/apprunner-demo)** - Containerized application deployment on App Runner.
- **[Amazon App Runner Deploy](https://github.com/awslabs/amazon-app-runner-deploy)** - GitHub integration for AWS App Runner deployments.
- **[Compose to Batch](https://github.com/turnerlabs/compose-to-batch)** - Transform docker-compose.yml into AWS Batch job definitions.
- **[EC2 Metadata in Docker](https://github.com/turnerlabs/ectou-metadata)** - EC2 instance metadata mocking service.

## Developer Productivity Tools

### Go Tools & Libraries
I have created numerous tools in Go to solve common development challenges:
- **[Go HTMX Tailwind Example](https://github.com/jritsema/go-htmx-tailwind-example)** - Example CRUD app showcasing Go + HTMX + Tailwind CSS.
- **[Gotoolbox](https://github.com/jritsema/gotoolbox)** - A collection of useful Go tools that use only the standard library, with no external dependencies.
- **[S3lib](https://github.com/jritsema/s3lib)** - Simplified Go library for S3 operations.
- **[Scaffolder](https://github.com/jritsema/scaffolder)** - Go library for tools that generate files and directory structures.
- **[SecretsManager Sidecar](https://github.com/turnerlabs/secretsmanager-sidecar)** - An elegant solution for managing AWS Secrets in containerized environments.
- **[Default Backend](https://github.com/jritsema/defaultbackend)** - Simple HTTP server for health checks and default responses.
- **[KPL Server](https://github.com/turnerlabs/kplserver)** - Multi-language support for the Amazon Kinesis Producer Library, which is written in Java.
- **[KPL Client Go](https://github.com/turnerlabs/kplclientgo)** - Go client library for KPL Server.
- **[Protonizer](https://github.com/awslabs/protonizer)** - CLI tool for AWS Proton Infrastructure as Code.

### Project Templates
Battle-tested starter templates that accelerate development:
- **[Cookiecutter Python](https://github.com/jritsema/cookiecutter-python)** - Modern Python project scaffolding.
- **[Python Template](https://github.com/jritsema/python-template)** - Quick-start Python project structure.
- **[Go Template](https://github.com/jritsema/go-template)** - Quick-start Go project structure.
- **[Terraform Starter](https://github.com/jritsema/terraform-starter)** - Production-ready Terraform project foundation.
- **[Lambda Python Template](https://github.com/jritsema/lambda-python-template)** - Streamlined AWS Lambda development in Python.

## AWS Cloud Architecture
Solutions and reference implementations for various cloud architecture patterns:

- **[PDF/Video Extraction Pipeline](https://github.com/jritsema/aws-pdf-video-extraction-pipeline)** - An automated content extraction system using AWS services.
- **[Doppler](https://github.com/WarnerMedia/doppler)** - A high-scale registration service showcasing AWS scalability.
- **[Lambda FURL TF](https://github.com/jritsema/lambda-furl-tf)** - A simple Lambda URL implementation using Terraform.
- **[Proton CodeBuild Examples](https://github.com/aws-containers/proton-codebuild-provisioning-examples/tree/main/terraform)** - Sample templates for AWS Proton with CodeBuild.
- **[Rekognize](https://github.com/jritsema/rekognize)** - CLI wrapper for the AWS Rekognition API.
- **[SAML Keygen](https://github.com/turnerlabs/samlkeygen)** - An authentication tool for AWS using the ADFS SAML provider.

## Container Orchestration
Tools for container management and deployment:
- **[Harbor](https://github.com/turnerlabs/harbor)** - An abstraction layer for container orchestration systems.
- **[Harbor Compose](https://github.com/turnerlabs/harbor-compose)** - A Docker Compose-like tool for Harbor deployments (written in Go).
- **[Harbor Terraform Provider](https://github.com/turnerlabs/terraform-provider-harbor)** - Use Terraform to manage Harbor applications (written in Go).

---

🔧 **My Development Environment**: Check out my [dotfiles](https://github.com/jritsema/home) to see how I set up my development environment.