---
title: "MCP CLI"
date: 2025-05-04T12:00:00Z
og_image: "https://raw.githubusercontent.com/modelcontextprotocol/.github/refs/heads/main/profile/assets/light.png"
summary: "This post introduces MCP CLI, a tool for managing MCP server configuration files"
---

If you're in the IT industry, you've likely heard of MCP, or [Model Context Protocol](https://modelcontextprotocol.io/). This emerging protocol, initially introduced by [Anthropic](https://www.anthropic.com/), is experiencing massive growth in adoption as it allows third parties to extend the power of large language models (LLMs) by giving them access to the outside world through the use of MCP servers. I'm not going to cover MCP in this post, however, it's important to note that number of MCP servers have proliferated across the industry since the [release of the MCP specification in November 2024](https://www.anthropic.com/news/model-context-protocol), . Here is a small sample of places where you can find MCP servers:

- MCP Repo: https://github.com/modelcontextprotocol/servers
- Smithery: https://smithery.ai
- Glama.ai: https://glama.ai/mcp/servers
- Awesome MCP Servers: https://mcpservers.org

### Pain Points

Over the past few months, I've encountered several pain points while experimenting with this MCP server technology:

- Manually editing JSON configuration files
- Managing similar configurations across different AI tools ([Amazon Q](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line.html), [Claude Desktop](https://modelcontextprotocol.io/quickstart/user), [Cursor](https://www.cursor.com/), etc.)
- Handling secret or sensitive environment variables
- Difficulty experimenting with new MCP servers
- Switching between different configurations based on context (programming, research, writing, etc.)

### Introducing [MCP CLI](https://github.com/jritsema/mcp-cli)

To address these pain points, I ["vibe coded"](https://x.com/karpathy/status/1886192184808149383) a tool over the weekend that aims to improve the user experience. When you look at the MCP JSON format, you'll notice that it resembles the [Docker Compose format](https://docs.docker.com/reference/compose-file/). Years of working with Docker and containers likely influenced my thinking around leveraging this format for configuring MCP servers. It turns out that the Docker Compose specification already has support for writing down [commands](https://docs.docker.com/reference/compose-file/services/#command), [images](https://docs.docker.com/reference/compose-file/services/#image), [environment](https://docs.docker.com/reference/compose-file/services/#environment) variables, and even [labels](https://docs.docker.com/reference/compose-file/services/#labels) for adding metadata like profiles. I wrote a specification for what I wanted the CLI tool to do and then used [Amazon Q Developer CLI](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/command-line-mcp.html) to vibe code it.

### Key Features

- **Centralized configuration**: A single configuration file can be shared and synchronized across multiple machines, exporting to various AI tools as needed. The configuration is stored in an `mcp-compose.yml` file.

- **Tool shortcuts for popular AI assistants**: MCP CLI provides shortcuts for exporting configurations to popular tools and allows setting custom locations.

- **Profile-based management**: Organize multiple MCP servers by tagging them with profiles, enabling easy configuration switching for different contexts.

- **Easy listing, setting, and clearing of configurations**: Use the CLI to examine configurations and profiles and then export them accordingly.

- **Support for command-based and container-based MCP servers**: Since MCP is agnostic to the local server process, a mix of custom binaries, package managers (e.g., uvx, npx, etc.), and container runtimes (e.g., docker, podman, finch, etc.) are supported. When leveraging containers, you can use `docker compose pull -f mcp-compose.yml` to pre-fetch container images from registries (Note that you have to add `build: .` to any command-based servers).

- **Secrets management**: Use [Docker Compose](https://docs.docker.com/compose/how-tos/environment-variables/set-environment-variables/) semantics to source secrets, like API keys and passwords, from external files and envvars, keeping them separate and secure while allowing your `mcp-compose.yml` file to be shared freely.

### Getting Started

To try [MCP CLI](https://github.com/jritsema/mcp-cli), download it from the latest [GitHub release](https://github.com/jritsema/mcp-cli/releases). After selecting your platform (Mac and Linux only for now) and unzipping the binary, rename it to `mcp` and place it in your path.

First, set your target MCP JSON file. If using Amazon Q CLI (you can use it for any MCP host tool), use the following command:

```sh
mcp config set tool ~/.aws/amazonq/mcp.json
```

Next, set up your MCP servers in the `mcp-compose.yml` file. Here is an example:

```sh
cat << EOF > ~/.config/mcp/mcp-compose.yml
services:
  time:
    command: uvx mcp-server-time --local-timezone=America/New_York
  fetch:
    command: uvx mcp-server-fetch
    labels:
      mcp.profile: web
EOF
```

Examine the configuration using the CLI:

```sh
# list default mcp servers
mcp ls

NAME  PROFILES  COMMAND                                                ENVVARS
----  --------  -------                                                -------
time  default   uvx mcp-server-time --local-timezone=America/New_York
```

```sh
# list all mcp servers
mcp ls -a

NAME   PROFILES  COMMAND                                                ENVVARS
----   --------  -------                                                -------
time   default   uvx mcp-server-time --local-timezone=America/New_York  
fetch  web       uvx mcp-server-fetch
```

Now, set up Amazon Q CLI with the default configuration:

```sh
mcp set
Wrote /Users/john/.aws/amazonq/mcp.json
```

You can give Claude Desktop the ability to fetch web content, for example:

```sh
mcp set web -t claude-desktop
Wrote /Users/john/Library/Application Support/Claude/claude_desktop_config.json
```

If you want to switch back to your default configuration, simply run:

```sh
mcp set -t claude-desktop
```

Note that you can source environment variables from the local environment or a `.env` file, for example:

```yaml
services:

  github-docker:
    image: ghcr.io/github/github-mcp-server
    environment:
      GITHUB_PERSONAL_ACCESS_TOKEN: ${GITHUB_PERSONAL_ACCESS_TOKEN}
    labels:
      mcp.profile: programming, docker

  brave:
    image: mcp/brave-search
    environment:
      BRAVE_API_KEY: ${BRAVE_API_KEY}
    labels:
      mcp.profile: programming, research
```

You can tag MCP servers in `mcp-compose.yml` using the `mcp.profile` label and switch between them easily for testing and experimentation. I hope this gives you insight into the tool and the problems it addresses. Check out the [GitHub repository](https://github.com/jritsema/mcp-cli) for more documentation and share your thoughts.
