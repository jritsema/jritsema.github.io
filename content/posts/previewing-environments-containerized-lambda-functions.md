---
title: Previewing environments using containerized AWS Lambda functions
date: 2023-02-06T12:00:00Z
---

I wrote [this post](https://aws.amazon.com/blogs/compute/previewing-environments-using-containerized-aws-lambda-functions/) based on a solution I provided to a customer. It explains how to set up ephemeral environments for pull requests (PRs) in CI/CD pipelines using containerized AWS Lambda functions. These environments allow teams to preview and collaborate on changes before merging them into the main codebase, reducing costs and improving efficiency. The [sample code](https://github.com/aws-samples/ephemeral-preview-containers-furl) uses [GitHub Actions](https://github.com/features/actions) to build, deploy, and manage a web application in a scalable and low-cost Lambda environment with [function URLs](https://docs.aws.amazon.com/lambda/latest/dg/lambda-urls.html). The ephemeral nature ensures that resources are provisioned quickly for testing and de-provisioned after the PR is closed, making this approach ideal for collaborative and cost-effective development workflows.

https://github.com/aws-samples/ephemeral-preview-containers-furl

[![AWS Blog Post](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2023/02/03/01-Picture.png)](https://aws.amazon.com/blogs/compute/previewing-environments-using-containerized-aws-lambda-functions/)
