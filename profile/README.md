# Composite Agent Runtime Environment (CARE)


**A framework for building, packaging, deploying, and orchestrating stateful AI agents**

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Work%20In%20Progress-yellow.svg)]()
[![Version](https://img.shields.io/badge/Spec%20Version-0.1-orange.svg)]()


---

> **WORK IN PROGRESS NOTICE**: The CARE framework is currently in early development (v0.1). Specifications and implementations are subject to significant changes. We welcome contributions, feedback, and participation in shaping this standard.

---

## CARE: Docker for AI Agents

Just as Docker revolutionized application deployment with containers, CARE aims to standardize AI agent deployment with agent bundles:

| Docker Concept | CARE Equivalent | Description |
|----------------|-----------------|-------------|
| **Dockerfile** | Agent definition files | Configuration files that define how to build an agent |
| **Docker Image** | Agent bundle | Packaged agent with all dependencies, ready to be instantiated |
| **Container** | Agent instance | A running agent with isolated execution environment |
| **Container Registry** | Agent registry | Storage and distribution of agent bundles |
| **Container State** | Agent state | Persisted agent memory and runtime information |
| **Docker Compose** | Agent orchestration | Coordinate multiple agents working together |
| **Docker Volumes** | Shared resources | Resources that can be shared between multiple agents |
| **Docker CLI** | CARE CLI | Command-line tools for working with agents |

CARE brings the same benefits to AI agents that Docker brought to applications:
- **Portability**: Build once, run anywhere
- **Isolation**: Self-contained environments
- **Standardization**: Common interface across platforms
- **Versioning**: Track changes to agent definitions
- **Composition**: Build complex systems from simple components

## Table of Contents

- [Introduction](#introduction)
- [Core Concepts](#core-concepts)
- [Framework Architecture](#framework-architecture)
  - [Agent Bundles](#agent-bundles)
  - [State Management](#state-management)
  - [Agent Orchestration](#agent-orchestration)
  - [Shared Resources](#shared-resources)
  - [Runtime Environment](#runtime-environment)
- [Repositories](#repositories)
- [Use Cases](#use-cases)
- [Getting Started](#getting-started)
- [Documentation](#documentation)
- [Specification](#specification)
- [Implementation Status](#implementation-status)
- [Community](#community)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Introduction

The Composite Agent Runtime Environment (CARE) is an open-source framework for creating self-contained, portable AI agent ecosystems. CARE addresses a critical gap in the AI agent ecosystem: the lack of a standardized way to package, deploy, and orchestrate stateful AI agents. Current approaches to agent development often result in tightly coupled, environment-dependent systems that are difficult to share, reuse, and compose.

CARE treats AI agents like containerized applications - they can be versioned, shared, composed into workflows, and migrated between environments while preserving their state. This approach enables the creation of complex, multi-agent systems from independent, specialized components.

Our mission is to create a standard that enables AI agents to be built once and run anywhere, with seamless composition, state preservation, and resource sharing.

## Core Concepts

The CARE framework is built around the following core concepts:

1. **Agent Bundles**: Self-contained packages including everything needed to instantiate an agent, similar to container images.

2. **State Management**: Mechanisms for capturing, persisting, and restoring agent state, enabling agents to be paused, transferred, and resumed.

3. **Agent Orchestration**: Tools and specifications for composing multiple agents into coordinated workflows.

4. **Shared Resources**: Systems for efficiently sharing tools, knowledge, and models between agents.

5. **Runtime Environment**: A standardized execution environment that can run agent bundles in a variety of deployment scenarios.

## Framework Architecture

### Agent Bundles

Agent bundles are self-contained packages that include all the components necessary to instantiate and run an AI agent:

```
my-agent.bundle/
├── agent.json            # Core agent definition
├── models/               # Optional bundled models
│   ├── primary.safetensors  # Main reasoning model (optional)
│   └── embeddings.bin    # Embedding model (optional)
├── knowledge/
│   ├── documents/        # Preprocessed documents
│   │   └── doc1.pdf
│   ├── embeddings/       # Pre-computed embeddings
│   │   └── doc1.embeddings
│   └── vectors.db        # Vector store for semantic search
├── tools/
│   ├── definitions.json  # Tool schemas and metadata
│   ├── scripts/          # Implementation scripts for custom tools
│   │   ├── search.py
│   │   └── calculator.py
│   └── dependencies.txt  # External dependencies needed by tools
├── runtime/
│   ├── environment.json  # Environment variable definitions
│   ├── security.json     # Permissions and access controls
│   └── sandbox.json      # Sandbox configuration for tool execution
└── manifest.json         # Overall bundle manifest with versioning, requirements
```

Bundles can be created, shared, versioned, and instantiated by CARE-compatible runtimes. They provide all the static components required to create a running agent instance.

### State Management

CARE provides mechanisms for capturing, storing, and restoring agent state, enabling capabilities like:

- Pausing and resuming agent execution
- Transferring agents between environments
- Creating snapshots and rollbacks
- Cloning agents with their accumulated knowledge

The state model captures essential runtime information:

```
my-agent.state/
├── instance_id.json      # Unique identifier and creation metadata
├── memory/
│   ├── core_memory.json  # Current core memory blocks
│   ├── archival/         # Long-term archival memory
│   └── conversations/    # Conversation history
├── tool_state/           # State maintained by tools
│   ├── search_history.json
│   └── custom_tool_db.sqlite
├── runtime_cache/        # Runtime optimization data
│   └── recent_embeddings.bin
└── checkpoint.json       # Metadata about when state was captured
```

### Agent Orchestration

CARE enables the composition of multiple specialized agents into coordinated workflows:

```
my-agent-ecosystem/
├── agents/
│   ├── primary-agent.bundle/   # Main orchestrating agent
│   ├── research-agent.bundle/  # Specialized research agent
│   └── coding-agent.bundle/    # Specialized coding agent
├── shared-resources/
│   ├── knowledge/              # Shared knowledge base
│   └── tools/                  # Common tools
├── communication/
│   ├── protocols.json          # Message format standards
│   ├── endpoints.json          # How agents discover each other
│   └── auth.json               # Inter-agent authentication
├── orchestration/
│   ├── workflow.json           # Agent interaction patterns
│   ├── service-map.json        # Agent capabilities registry
│   └── fallback.json           # Error handling between agents
└── manifest.json               # Ecosystem-level metadata
```

Orchestration enables:
- Agent-to-agent communication
- Workflow-based execution patterns
- Specialized agent roles within larger systems
- Resilient multi-agent architectures

### Shared Resources

CARE provides a resource sharing system to avoid duplication and enable efficient collaboration between agents:

```
shared-resources/
├── registry.json           # Central registry of all shared resources
├── documents/
│   ├── document-1.pdf      # Original documents
│   └── document-registry.json  # Metadata and access control
├── embeddings/
│   ├── embedding-pools/    # Pre-computed embeddings
│   └── vector-stores/      # Shared vector databases
├── tools/
│   ├── common-tools/       # Implementation of shared tools
│   └── tool-registry.json  # Tool versioning and compatibility
└── models/
    ├── shared-models/      # Models that can be shared
    └── model-registry.json # Model metadata and requirements
```

Resources are referenced using a URI system:

```json
{
  "knowledge_sources": [
    {
      "type": "document",
      "uri": "resource://documents/financial-report-2023",
      "access_mode": "read_only"
    }
  ]
}
```

### Runtime Environment

The CARE runtime provides a standardized execution environment for agent bundles, handling:

- Bundle loading and validation
- Model initialization and operation
- Tool execution in secure sandboxes
- State management operations
- Inter-agent communication
- Resource allocation and management

The runtime interface provides a consistent API across different deployment scenarios, from local development to cloud deployment.

## Repositories

| Repository | Description |
|------------|-------------|
| [spec](https://github.com/care-framework/spec) | Core specifications for the CARE standard |
| [runtime](https://github.com/care-framework/runtime) | Reference implementation of the CARE runtime |
| [cli](https://github.com/care-framework/cli) | Command-line tools for working with CARE bundles |
| [examples](https://github.com/care-framework/examples) | Example agent bundles and orchestration patterns |
| [web](https://github.com/care-framework/web) | Web interface for managing CARE agents |
| [sdk](https://github.com/care-framework/sdk) | SDKs for building CARE-compatible agents |

## Use Cases

- **Agent Portability**: Package agents to run consistently across development, testing, and production
- **Stateful Migration**: Move agents between environments without losing context or memory
- **Team Collaboration**: Share agents with predictable behavior across development teams  
- **Composite Workflows**: Build complex agent systems from simpler, specialized components
- **Resource Optimization**: Efficiently share tools and knowledge across multiple agents

## Getting Started

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

## Documentation

For full documentation, visit [care-framework.github.io/docs](https://care-framework.github.io/docs).

- [Core Concepts](https://care-framework.github.io/docs/concepts)
- [Bundle Format Specification](https://care-framework.github.io/docs/spec/bundle)
- [Tool Development Guide](https://care-framework.github.io/docs/tools)
- [Agent Orchestration](https://care-framework.github.io/docs/orchestration)
- [API Reference](https://care-framework.github.io/docs/api)

## Specification

### Bundle Format

The agent bundle format consists of the following key components:

#### Manifest File (`manifest.json`)

```json
{
  "format_version": "0.1",
  "bundle_id": "research-assistant-v1",
  "name": "Research Assistant",
  "description": "An agent specialized in online research tasks",
  "version": "1.2.3",
  "created_at": "2025-04-07T10:30:00Z",
  "authors": ["CARE Framework Team"],
  "license": "Apache-2.0",
  "requirements": {
    "runtime_version": ">=0.5.0",
    "memory": "1Gi",
    "compute": "2 cores"
  },
  "entry_points": {
    "default": "agent.json",
    "cli": "cli_interface.json"
  }
}
```

#### Agent Definition (`agent.json`)

```json
{
  "agent_type": "llm_agent",
  "llm_config": {
    "model_id": "models/primary",
    "model_reference": "openai/gpt-4o",
    "temperature": 0.7,
    "max_tokens": 4096,
    "context_window": 32000
  },
  "embedding_config": {
    "model_id": "models/embeddings",
    "model_reference": "openai/text-embedding-ada-002", 
    "dimensions": 1536
  },
  "system_prompt": "You are a specialized research assistant...",
  "tools": [
    {
      "id": "web_search",
      "definition_path": "tools/definitions/web_search.json",
      "implementation_path": "tools/scripts/web_search.py",
      "permissions": ["network:outbound"]
    }
  ],
  "knowledge_sources": [
    {
      "id": "research_guidelines",
      "path": "knowledge/documents/guidelines.pdf"
    }
  ],
  "memory_configuration": {
    "core_memory_schema": [
      {
        "label": "persona",
        "description": "Agent's persona and behavior",
        "limit": 5000
      }
    ]
  }
}
```

### State Format

The state format captures the dynamic aspects of a running agent:

#### Instance Metadata (`instance_id.json`)

```json
{
  "instance_id": "research-assistant-9f8a3b2c",
  "created_from_bundle": "research-assistant-v1",
  "bundle_version": "1.2.3",
  "created_at": "2025-04-07T14:22:15Z",
  "runtime_version": "0.5.2",
  "host_info": {
    "platform": "linux",
    "hostname": "research-server-12"
  }
}
```

### Orchestration Format

The orchestration format defines how multiple agents interact:

#### Workflow Definition (`orchestration/workflow.json`)

```json
{
  "workflow_id": "customer_query_handler",
  "version": "1.0.0",
  "description": "Process customer queries with specialized agents",
  "steps": [
    {
      "id": "parse_query",
      "agent": "primary-agent",
      "action": "parse_query",
      "next": {
        "condition": "query.type == 'research'",
        "true": "research_step",
        "false": "coding_step"
      }
    },
    {
      "id": "research_step",
      "agent": "research-agent",
      "action": "deep_research",
      "next": "synthesis_step"
    },
    {
      "id": "coding_step",
      "agent": "coding-agent",
      "action": "generate_code",
      "next": "synthesis_step"
    },
    {
      "id": "synthesis_step",
      "agent": "primary-agent",
      "action": "synthesize_results"
    }
  ]
}
```

## Implementation Status

The CARE framework is currently in early development (v0.1). The following components are in progress:

| Component | Status | Target Completion |
|-----------|--------|-------------------|
| Core Specifications | 🟡 In Progress | Q2 2025 |
| Reference Runtime | 🔴 Planning | Q3 2025 |
| CLI Tools | 🔴 Planning | Q3 2025 |
| Bundle Format | 🟡 In Progress | Q2 2025 |
| State Management | 🟡 In Progress | Q2 2025 |
| Orchestration | 🔴 Planning | Q4 2025 |
| Resource Registry | 🔴 Planning | Q4 2025 |

## Community

- [Discord Server](https://discord.gg/careframework)
- [Contribution Guidelines](CONTRIBUTING.md)
- [Code of Conduct](CODE_OF_CONDUCT.md)

## Contributing

We welcome contributions to the CARE framework! Here's how you can help:

1. **Feedback on Specifications**: Review and comment on the draft specifications
2. **Use Case Submissions**: Share examples of how you would use CARE
3. **Implementation Work**: Help build the reference runtime or tools
4. **Documentation**: Improve explanations and examples

Please see [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

## License

CARE is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

This license allows:
- Commercial use
- Modification
- Distribution
- Patent use
- Private use

While requiring:
- License and copyright notice
- State changes made to the code

The Apache License 2.0 was chosen to promote widespread adoption while ensuring proper attribution and providing patent protections.

## Acknowledgements

CARE builds on ideas from container technologies like Docker, agent frameworks like LangChain and AutoGPT, and orchestration systems like Kubernetes. We're grateful to all the pioneers in these fields whose work has inspired this project.
