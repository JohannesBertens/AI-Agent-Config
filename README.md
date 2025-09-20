# AI-Agent-Config
Public repo to share findings on using AI Agents for Coding.
There's quite a few. Not all great. Not all bad.

## Definition
First off: what is my definition of an AI Agent?
- Runs either in a IDE or stand-alone as tool on the command line (CLI) -- I prefer the CLI variant
- Connects to (or is a) LLM that can transform natural language commands into output and interact with the codebase
- Can use tools (like MCP) to improve the outcome

Well, that's pretty broad still. I've tried a few, but these are the ones I'm seriously using:
- Claude Code
- Codex
- Code(r) (fork of Codex)
- Gemini
- Qwen (fork of Gemini)
- Roo Code

## The Agents
### Claude Code
Pros:
- Fast
- Very decent code quality
- Very populair, so a lot of information to be found online
- Great at searching online for information
Cons:
- Runs through the "limits" quickly
- Hard(er) to configure with alternative LLMs
- Keeps forgetting/losing my configuration

### Codex & Coder
**Codex**
Github: https://github.com/openai/codex
Pros:
- Fast
- Feels limited in usage
Cons:
- Runs through the "limits" quickly
- NEEDS "--search" when using or it will not search online

**Code(r)**
Github: https://github.com/just-every/code

Pros:
- Can call other agents (Claude, Code, Gemini, Qwen)
- Seems to work well with GTP-5
- Uses tokens quickly
- A lot of options to configure
Cons:
- A lot of options to configure
- Does not work well with other LLMs via OpenRouter

How to configure a different provider:
Open `~/.codex/config.toml` and change the model & provider as such
```
model= "openai/gpt-5"
model_provider = "openrouter"
preferred_auth_method = "apikey"
model_reasoning_effort = "medium"

[model_providers.openrouter]
name = "openrouter"
base_url = "https://openrouter.ai/api/v1"
env_key= "OPENROUTER_API_KEY"
```
Then run `export OPENROUTER_API_KEY=<your key here>` after which you can start `codex`, `code` or `coder` depending on your preference and installation.

MCP servers are also configured _differently_ here.
```
[mcp_servers.context7]
args = ["-y", "@upstash/context7-mcp", "--api-key", "<API KEY HERE>"]
command = "npx"

[mcp_servers.playwright]
command = "npx"
args = ["@playwright/mcp@latest"]

[mcp_servers.nextjs_docs]
command = "npx"
args = ["mcp-remote","https://gitmcp.io/vercel/next.js" ]

[mcp_servers.tailwindcss_docs]
command = "npx"
args = ["mcp-remote","https://gitmcp.io/tailwindlabs/tailwindcss" ]

[mcp_servers.fastapi_docs]
command = "npx"
args = ["mcp-remote","https://gitmcp.io/fastapi/fastapi" ]

[mcp_servers.pydantic_ai_docs]
command = "npx"
args = ["mcp-remote","https://gitmcp.io/pydantic/pydantic-ai" ]

[mcp_servers.postgres_docs]
command = "npx"
args = ["mcp-remote","https://gitmcp.io/postgres/postgres" ]
```
### Gemini
Pros:
- Can use the "gemini-2.5-flash" model pretty much all day
- Can search online great
Cons:
- In the free tier, the "gemini-2.5-pro" model (default) runs out of tokens very quickly
- A bit slow
- Is lagging behind on ohter updated agents a bit

### Qwen / Qwen Code
Github: https://github.com/QwenLM/qwen-code
Pros:
- Runs the Qwen3 Coder model once logged in forever
Cons:
- A bit slow
- Not much to configure
- Feels behind compared to recent updates on other agents

### Roo Code
Pros:
- A lot to configure
- Has a decent Todolist, like Claude Code
Cons:
- Slow
- Only available in the IDE, no CLI
