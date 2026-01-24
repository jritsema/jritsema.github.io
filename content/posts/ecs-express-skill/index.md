---
title: "ECS Express: Agent Skill"
date: 2026-01-23T12:00:00Z
og_image: "https://johnritsema.com/posts/ecs-express-skill/skill-install.png"
summary: "I adapted my ECS Express Kiro Power into an Agent Skill that works with any agentic AI tool. Here's how the Agent Skills standard enables portable deployment workflows."
---

## Portability

In my [last post](/posts/ecs-express-kiro-power/), I built a [Kiro Power](https://kiro.dev/powers/) for deploying apps to [AWS ECS Express Mode](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/express-service-overview.html). It worked great in Kiro, but what about developers using _amp, antigravity, claude-code, codex, cursor, gemini-cli, github-copilot, goose, kiro-cli, opencode_, and the dozens of others?

The knowledge encoded in that power (how to infer app config, which APIs to call, how to monitor deployments, how to make optimizations) shouldn't be confined to a single tool. That's where **Agent Skills** comes in.

## What Are Agent Skills?

[Agent Skills](https://agentskills.io/) is an [open standard proposed by Anthropic](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills) for packaging agent knowledge in a portable format. The core idea: a `SKILL.md` file with YAML frontmatter containing metadata, plus markdown instructions the agent follows. That's it. Very simple.

```yaml
---
name: "ecs-express"
displayName: "Deploy Web Apps and APIs to AWS using ECS Express Mode"
description: "Assists with deploying a web app or API to AWS..."
keywords: ["ecs", "express", "deploy", "aws", "container", "fargate"]
author: "John Ritsema"
license: MIT-0
---
## Overview
...instructions...
```

When you install a skill, the agent loads only the metadata initially. When a task matches the skill's keywords or description, the full instructions load into context. This is the _progressive disclosure_ pattern I mentioned before - keeping the agent focused until it needs specific knowledge.

## Adapting the Power to a Skill

The conversion was simple. My Kiro Power already had a `POWER.md` with structured instructions. The main changes:

1. **Created a `skill/SKILL.md`** with the Agent Skills frontmatter format
2. **Removed MCP-specific dependencies** - Skills rely on the host agent's tool access rather than bundled MCP servers
3. **Added tool validation** - Since skills can't guarantee MCP server availability, the instructions now check for AWS CLI and Docker CLI upfront

## The Key Difference: Tools

Kiro Powers can bundle [MCP server configurations](https://kiro.dev/docs/powers/create/#adding-mcp-servers), similar to [Claude Plugins](https://code.claude.com/docs/en/plugins). My ECS Express Power includes the [AWS API MCP server](https://awslabs.github.io/mcp/servers/aws-api-mcp-server), which calls AWS APIs directly without needing the AWS CLI installed.

Agent Skills are tool-agnostic. They assume the host agent has access to shell commands, so the skill instructions use the AWS CLI instead. This means users need the AWS CLI installed, but it also means the skill works anywhere.

## Installing the Skill

The [skills CLI](https://skills.sh/) created by [Vercel](https://vercel.com/changelog/introducing-skills-the-open-agent-skills-ecosystem) makes installation simple:

```sh
npx skills add jritsema/ecs-express-power
```

```sh
███████╗██╗  ██╗██╗██╗     ██╗     ███████╗
██╔════╝██║ ██╔╝██║██║     ██║     ██╔════╝
███████╗█████╔╝ ██║██║     ██║     ███████╗
╚════██║██╔═██╗ ██║██║     ██║     ╚════██║
███████║██║  ██╗██║███████╗███████╗███████║
╚══════╝╚═╝  ╚═╝╚═╝╚══════╝╚══════╝╚══════╝


┌   skills
│
◇  Source: https://github.com/jritsema/ecs-express-power.git
│
◇  Repository cloned
│
◇  Found 1 skill
│
●  Skill: ecs-express
│
│  Assists with deploying a web app or API to AWS using Amazon ECS Express Mode. ECS Express Mode takes your container image and gives you back an HTTPS endpoint
│
◇  Detected 5 agents
│
◇  Select agents to install skills to
│  Claude Code, Cursor, Goose, Kiro CLI, OpenCode
│
```

The skill is now available to any of the [supported agents](https://github.com/vercel-labs/add-skill?tab=readme-ov-file#available-agents).

Note that the Skills CLI automatically detects which agents you have installed by checking for their configuration directories. If none are detected, you'll be prompted to select which agents to install to.

### Claude Code

Here's a snippet of how it looks using Claude Code.

```
...

⏺ Bash(curl -I https://si-9c1a1d7cd98a4a96b9410ef080072c63.ecs.us-east-1.on.aws/health)
  ⎿  HTTP/2 200
     date: Thu, 22 Jan 2026 23:00:39 GMT
     content-type: text/html; charset=utf-8
     … +8 lines (ctrl+o to expand)

⏺ Perfect! The service is up and running. Let me test the main endpoint as well.

⏺ Bash(curl https://si-9c1a1d7cd98a4a96b9410ef080072c63.ecs.us-east-1.on.aws/)
  ⎿  <!DOCTYPE html>
     <html lang="en">
       <head>
     … +27 lines (ctrl+o to expand)

⏺ Deployment successful! Your app is live and running on AWS ECS Express Mode.

  Service Details:
  - Endpoint: https://si-9c1a1d7cd98a4a96b9410ef080072c63.ecs.us-east-1.on.aws
  - Service name: simple-app
  - Cluster: default
  - CPU: 1024
  - Memory: 2048 MB
  - Health check: /health (returning HTTP 200)
  - Scaling: 1-10 containers (autoscaling on 60% CPU)

  Your app is responding correctly on both the health check endpoint and the main page.

  Note: ECS Express Mode defaults to blue/green canary deployments which can take up to 10 minutes for updates. If you'd like faster deployments in the
  future, I can speed this up by reducing bake time and traffic shifting intervals.
```

## Why This Matters

The Agent Skills standard solves a problem: knowledge portability. As the AI coding assistant landscape fragments across _Kiro, Claude Code, Amp, Antigravity, Cursor, Gemini CLI_, and others, developers shouldn't have to rebuild their workflows for each tool.

Skills let you:

- **Write once, run anywhere** - Same instructions work across compatible agents
- **Share knowledge** - Publish skills for others to use
- **Avoid lock-in** - Switch tools without losing your custom workflows

## Try It

If you're using Kiro CLI, Claude Code, or another agent that supports skills:

```
npx skills add jritsema/ecs-express-power
```

Then ask your agent to deploy your app to ECS Express.

The repo is open source: [github.com/jritsema/ecs-express-power](https://github.com/jritsema/ecs-express-power)

Let me know how it goes, especially if you try it with an agent I haven't tested yet.
