# BytePlus IGA Pages Agent Plugin

Develop and deploy frontend, full-stack, and AI agent applications on [BytePlus IGA Pages](https://docs.byteplus.com/en/docs/iga) with your AI coding agent.

## Getting Started

### Supported Tools

The repository includes integration files for these clients:

| Tool | Status |
| --- | --- |
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | Supported |
| [Gemini CLI](https://geminicli.com) | Supported |
| [OpenAI Codex](https://openai.com/index/codex/) | Supported |
| [Cursor](https://www.cursor.com) | Supported |
| [Kilo](https://kilo.ai) | Supported |
| [OpenCode 2](https://opencode.ai) | Supported |
| [Grok Build](https://x.ai/news/grok-build-cli) | Supported |
| [GitHub Copilot CLI](https://github.com/github/copilot-cli) | Supported |
| [Kimi Code](https://kimi.com) | Supported |

Hook activation depends on the client's version, settings, and workspace policy.

### Prerequisites

- An AI coding tool that supports plugins or [Agent Skills](https://agentskills.io/).
- Node.js 20 or newer.
- A BytePlus IGA Pages account and CLI authentication for remote operations.

### Installation

Use a compatible plugin installer and select your client:

```bash
npx plugins add byteplus-sdk/byteplus-iga-pages-plugin
```

Restart your client after installation and approve hooks when prompted.

To install only the skill and reference files:

```bash
npx skills add byteplus-sdk/byteplus-iga-pages-plugin
```

Skill-only installation does not include development hooks or MCP configuration.

## What It Does

The plugin gives your agent BytePlus IGA Pages guidance for project setup, framework compatibility, local development, deployment, environment variables, integrations, and debugging. It also covers persistent conversations, sandboxed tools, and object storage for AI applications.

One entry-point skill routes the agent to the relevant reference files as needed.

## How Do I Use This?

Ask your agent to work on a BytePlus IGA Pages project. The agent can load the skill when your request matches its scope.

Deployment examples:

```text
Deploy my app to BytePlus IGA Pages and give me a preview URL.
```

```text
Can this app run on BytePlus IGA Pages? Check what needs to change.
```

Development examples:

```text
Build an AI agent on BytePlus IGA Pages with persistent conversations and sandboxed tools.
```

```text
Add an API to my BytePlus IGA Pages project and help me run it locally.
```

```text
Help me configure environment variables and connect Supabase for this project.
```

Debugging example:

```text
Inspect this BytePlus IGA Pages deployment and help me diagnose its runtime errors.
```

When enabled, the development hook reminds the agent to start the local development environment with `bp-iga pages dev` when it detects that the project needs the IGA development runtime. It is advisory: the agent still decides how to proceed.

## Components

### Skill

| Skill | Covers |
| --- | --- |
| [byteplus-iga-pages](skills/byteplus-iga-pages/SKILL.md) | CLI setup and authentication, project workflows, deployment, and routing to development references |

### Development Reminders

When the plugin detects that your project needs the IGA development runtime, the plugin reminds the agent to start the local development environment with `bp-iga pages dev`. OpenCode adds this guidance during the session. Gemini CLI checks at session startup, resume, or clear. Clients with terminal hooks check development commands. Reminders are advisory, may not recognize complex shell commands, and depend on your client's hook settings.

Keep `package.json` `scripts.dev` set to the framework command, such as `vite` or `next dev`, then run `bp-iga pages dev` in the terminal. Do not set `scripts.dev` to `bp-iga pages dev`: IGA invokes that script, causing recursive startup. Clients with terminal hooks check for this configuration when running commands such as `npm run dev` or `bp-iga pages dev` and prompt the agent to correct it.

## Ecosystem Coverage

- Frameworks: Next.js, Vite, Vue CLI, Create React App, Angular, Hexo, Docusaurus, VitePress, VuePress, Astro, Nuxt, and plain static assets.
- Functions: Node.js API routes, Web-standard handlers, Express, and Koa.
- AI applications: persistent conversations, OpenAI Agents sessions, LangGraph checkpoints, Claude session storage, and Sandbox tools.
- Storage: durable project-scoped Blob objects.
- CLI workflows: authentication, initialization, linking, local development, builds, deployment, environment variables, integrations, inspection, and logs.

## Usage Statistics

The plugin reports first use and daily activity by default. Events are sent to `https://sgali-mcs.byteoversea.com/list` in Singapore. Events include the plugin name/version, client type, and a hashed device identifier. Set `IGA_PAGES_PLUGIN_TELEMETRY_DISABLED=1` in the client environment to disable reporting. Network requests time out after one second; reporting failures do not fail the hook. Kimi does not register session hooks. OpenCode also supports the plugin option `telemetry: false` to disable reporting. Restart the OpenCode service after changing its environment (`opencode service restart`).

## License

[MIT](LICENSE)
