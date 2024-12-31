---
title: Architecting for resiliency on AWS App Runner
date: 2022-07-05T12:00:00Z
---

This is the first [blog post](https://aws.amazon.com/blogs/containers/architecting-for-resiliency-on-aws-app-runner/) I wrote as an AWS employee. It addresses how to design a resilient, multi-region architecture using App Runner for hosting containerized applications. It covers the use of Route 53 for traffic management and health checks, DynamoDB global tables for multi-region database replication, and ECR for cross-region container image replication.  The architecture ensures high availability and fault tolerance by setting up active-active configurations across two AWS regions, and automating deployments via CI/CD pipelines. The post includes [sample code](https://github.com/aws-samples/apprunner-multiregion) including Terraform for infrastructure as code (IaC), a Next.js frontend and a Go API server.

https://github.com/aws-samples/apprunner-multiregion

[![AWS Blog Post](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2022/07/01/apprunner-multi-region.jpg)](https://aws.amazon.com/blogs/containers/architecting-for-resiliency-on-aws-app-runner/)
