---
title: Simplify Your Bedrock Converse API Integration with the bedrock-tools Python Library
date: 2024-10-25T12:00:00Z
---

I wrote this [post](https://community.aws/content/2lG8i8QCsoqaZLi4XjSSt15gqTD) to introduce [bedrock-tools](https://github.com/jritsema/bedrock-tools), a [Python library](https://pypi.org/project/bedrock-tools/) I wrote to streamline the integration of custom Python functions with the [Amazon Bedrock Converse API](https://docs.aws.amazon.com/bedrock/latest/userguide/conversation-inference.html) for building conversational AI agents and applications. The library minimizes boilerplate code, automates type handling by generating JSON schemas from function annotations, and manages tool invocation and exception handling seamlessly. By enabling developers to define tools as simple Python functions, **bedrock-tools** simplifies the development process, allowing a focus on core application functionality.

Python library - https://github.com/jritsema/bedrock-tools

Post - https://community.aws/content/2lG8i8QCsoqaZLi4XjSSt15gqTD

#### Sample code

```sh
pip install bedrock-tools
```

```python
from bedrock_tools import BedrockTools

# define native functions as tools (using type annotations)

def add_numbers(a: int, b: int) -> int:
    """Add two numbers together."""
    return a + b


def greet(name: str) -> str:
    """Greet a person by name."""
    return f"Hello, {name}!"


def get_weather(city: str, state: str) -> dict:
    """Get the weather for a location."""
    return {
        "city": city,
        "state": state,
        "temperature": "75°F",
        "condition": "Partly Cloudy",
    }

# setup
tools = BedrockTools()
tools.add_function(add_numbers)
tools.add_function(greet)
tools.add_function(get_weather)

# Use the config in your Bedrock Converse API call
response = bedrock.converse(
    modelId=model_id,
    toolConfig=tools.get_tool_config()
    messages=messages,
)

# When you receive a toolUse from the API, invoke the tool
if "toolUse" in content_block:
    tool_results.append(tools.invoke(content_block["toolUse"]))

message = {"role": "user", "content": tool_results}
```

