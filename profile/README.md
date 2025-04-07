# Composite Agent Runtime Environment (CARE)


**A framework for building, packaging, deploying, and orchestrating stateful AI agents**

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)



## 🧠 What is CARE?

The Composite Agent Runtime Environment (CARE) is an open-source framework for creating self-contained, portable AI agent ecosystems. CARE treats AI agents like containerized applications - they can be versioned, shared, composed into workflows, and migrated between environments while preserving their state.

Our mission is to create a standard that enables AI agents to be built once and run anywhere, with seamless composition, state preservation, and resource sharing.

## 🔑 Key Concepts

- **Agent Bundles**: Self-contained packages including agent definition, tools, knowledge, and optionally models
- **Stateful Agents**: Checkpoint, resume, and transfer running agents with memory intact
- **Agent Orchestration**: Create complex workflows with multiple specialized agents
- **Shared Resources**: Efficiently share tools, documents, and models between agents
- **Portable Runtime**: Run the same agent bundle across different environments

## 🗂️ Repositories

| Repository | Description |
|------------|-------------|
| [spec](https://github.com/care-framework/spec) | Core specifications for the CARE standard |
| [runtime](https://github.com/care-framework/runtime) | Reference implementation of the CARE runtime |
| [cli](https://github.com/care-framework/cli) | Command-line tools for working with CARE bundles |
| [examples](https://github.com/care-framework/examples) | Example agent bundles and orchestration patterns |
| [web](https://github.com/care-framework/web) | Web interface for managing CARE agents |
| [sdk](https://github.com/care-framework/sdk) | SDKs for building CARE-compatible agents |

## 🛠️ Use Cases

- **Agent Portability**: Package agents to run consistently across development, testing, and production
- **Stateful Migration**: Move agents between environments without losing context or memory
- **Team Collaboration**: Share agents with predictable behavior across development teams  
- **Composite Workflows**: Build complex agent systems from simpler, specialized components
- **Resource Optimization**: Efficiently share tools and knowledge across multiple agents

## 📦 Getting Started

```bash
# Install the CARE CLI
npm install -g care-cli

# Create a new agent bundle
care init my-first-agent

# Run your agent
care run my-first-agent

# Create an agent checkpoint
care checkpoint my-first-agent --output my-agent.state

# Resume from checkpoint
care resume --from my-agent.state
```

## 📚 Documentation

For full documentation, visit [care-framework.github.io/docs](https://care-framework.github.io/docs).

- [Core Concepts](https://care-framework.github.io/docs/concepts)
- [Bundle Format Specification](https://care-framework.github.io/docs/spec/bundle)
- [Tool Development Guide](https://care-framework.github.io/docs/tools)
- [Agent Orchestration](https://care-framework.github.io/docs/orchestration)
- [API Reference](https://care-framework.github.io/docs/api)

## 👥 Community

- [Discord Server](https://discord.gg/careframework)
- [Contribution Guidelines](CONTRIBUTING.md)
- [Code of Conduct](CODE_OF_CONDUCT.md)

## 📝 License

CARE is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgements

CARE builds on ideas from container technologies like Docker, agent frameworks like LangChain and AutoGPT, and orchestration systems like Kubernetes. We're grateful to all the pioneers in these fields whose work has inspired this project.
