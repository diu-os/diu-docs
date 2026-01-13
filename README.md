# 📚 DIU OS Documentation

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Discord](https://img.shields.io/discord/YOUR_DISCORD_ID?color=7289da&label=Discord&logo=discord&logoColor=white)](https://discord.gg/diu-os)

> Official documentation for DIU OS — the Scientific Operating System for decentralized science.

## 🌐 Quick Links

| Resource | Link |
|----------|------|
| 🏠 Main Website | [diu-os.org](https://diu-os.org) |
| 👩‍💻 Developer Portal | [dev.diu-os.org](https://dev.diu-os.org) |
| 🔬 Physics Tutorial | [GitHub](https://github.com/diu-os/physics-tutorial) |
| 🤖 MCP Servers | [GitHub](https://github.com/diu-os/mcp-servers) |
| 💬 Community | [Discord](https://discord.gg/diu-os) |

---

## 📖 Documentation Structure

```
docs/
├── getting-started/
│   ├── introduction.md         # What is DIU OS?
│   ├── quick-start.md          # 5-minute setup guide
│   └── architecture-overview.md # High-level system design
│
├── tutorials/
│   ├── physics-simulation.md   # Building quantum simulations
│   ├── mcp-integration.md      # Connecting AI assistants
│   └── contributing.md         # How to contribute
│
├── api-reference/
│   ├── rest-api.md             # REST API endpoints
│   ├── websocket-api.md        # Real-time events
│   └── mcp-tools.md            # MCP server tools
│
├── architecture/
│   ├── system-design.md        # DDD & Event-Driven patterns
│   ├── cdc-pipeline.md         # Change Data Capture
│   └── security.md             # Security considerations
│
└── community/
    ├── code-of-conduct.md      # Community guidelines
    ├── roadmap.md              # Public roadmap
    └── faq.md                  # Frequently asked questions
```

---

## 🚀 Getting Started

### What is DIU OS?

DIU OS (DeSci Intelligent Universe Operating System) is an open-source platform for decentralized science, combining:

- **Real-time CDC Architecture** — Sub-100ms event streaming for collaborative research
- **AI-Powered Research Tools** — Model Context Protocol (MCP) integration for any LLM
- **Interactive Simulations** — WebAssembly-powered quantum physics experiments
- **Web3 Integration** — Blockchain-based reproducibility and IP protection

### Quick Start

```bash
# Clone the physics tutorial to explore DIU OS capabilities
git clone https://github.com/diu-os/physics-tutorial.git
cd physics-tutorial

# Install and run
npm install
npm run dev

# Open http://localhost:5173
```

### Core Concepts

#### Domain-Driven Design (DDD)

DIU OS is built on DDD principles with clear bounded contexts:

| Context | Responsibility |
|---------|---------------|
| **Identity** | User authentication, DIDs, profiles |
| **Research Objects** | Publications, datasets, versions |
| **Simulation** | Physics engines, visualizations |
| **Funding** | Grants, contributions, rewards |

#### Event-Driven Architecture

All state changes flow through our CDC pipeline:

```
Database Change → WAL Capture → ETL Transform → Redis Streams → WebSocket
```

This enables real-time collaboration with <100ms latency.

---

## 🏗️ Architecture Overview

### High-Level System Design

```
┌─────────────────────────────────────────────────────────────┐
│                     PRESENTATION LAYER                       │
│   Web Client │ Mobile Apps │ VR/AR Clients │ API Consumers  │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                        API GATEWAY                           │
│          Load Balancing │ Auth │ Rate Limiting               │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                    RUST MICROSERVICES                        │
│   Project  │  Simulation  │  AI Core  │  Funding            │
│   Service  │   Service    │  Service  │  Service            │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                     EVENT BUS (CDC)                          │
│          PostgreSQL WAL │ Redis Streams │ WebSocket          │
└─────────────────────────────────────────────────────────────┘
                              │
┌─────────────────────────────────────────────────────────────┐
│                      MCP SERVERS                             │
│   Physics  │  Knowledge  │  Progress  │  External           │
│   Server   │   Server    │   Server   │  Connectors         │
└─────────────────────────────────────────────────────────────┘
```

### Technology Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| Backend | Rust (Axum) | High-performance microservices |
| Frontend | React + TypeScript | Interactive UI |
| Database | PostgreSQL | Primary data store |
| Caching | Redis | Event streams & caching |
| Real-time | Supabase | CDC & authentication |
| AI | MCP Protocol | LLM integration |
| 3D | Three.js + WebGL | Physics visualizations |

---

## 📡 API Reference

### REST API

Base URL: `https://api.diu-os.org/v1`

#### Authentication

```bash
# All requests require Bearer token
curl -H "Authorization: Bearer YOUR_TOKEN" \
     https://api.diu-os.org/v1/projects
```

#### Endpoints Overview

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/projects` | List all projects |
| `POST` | `/projects` | Create new project |
| `GET` | `/simulations` | List simulations |
| `POST` | `/simulations/:id/run` | Execute simulation |
| `GET` | `/events/stream` | SSE event stream |

> 📝 **Note**: Full API documentation with request/response schemas available at [api.diu-os.org/docs](https://api.diu-os.org/docs)

### WebSocket API

Connect to real-time events:

```javascript
const ws = new WebSocket('wss://api.diu-os.org/v1/ws');

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  console.log('Event type:', data.type);
  console.log('Payload:', data.payload);
};

// Subscribe to specific events
ws.send(JSON.stringify({
  action: 'subscribe',
  channels: ['simulation:updates', 'project:changes']
}));
```

#### Event Types

| Event | Description |
|-------|-------------|
| `simulation:state_changed` | Simulation parameters updated |
| `simulation:result` | New simulation result available |
| `project:member_joined` | New collaborator joined project |
| `funding:contribution` | New funding contribution received |

---

## 🤖 MCP Integration

DIU OS uses [Model Context Protocol](https://modelcontextprotocol.io/) for AI integration, enabling any LLM to interact with our platform.

### Available MCP Servers

| Server | Tools | Description |
|--------|-------|-------------|
| Physics | `run_simulation`, `get_parameters` | Control physics simulations |
| Knowledge | `search_concepts`, `get_explanation` | Query knowledge base |
| Progress | `get_achievements`, `update_progress` | Track learning progress |

### Quick Integration

```typescript
// Connect MCP server to Claude Desktop
// Add to claude_desktop_config.json:
{
  "mcpServers": {
    "diu-physics": {
      "command": "npx",
      "args": ["-y", "@diu-os/mcp-physics"]
    }
  }
}
```

> 📘 See [MCP Servers repository](https://github.com/diu-os/mcp-servers) for full documentation.

---

## 🔐 Security

### Authentication

DIU OS supports multiple authentication methods:

- **JWT Tokens** — Standard API authentication
- **ORCID OAuth** — Academic identity verification
- **Web3 Wallets** — Decentralized authentication (coming soon)

### Data Protection

- All data encrypted at rest (AES-256)
- TLS 1.3 for all connections
- GDPR-compliant data handling
- Row-Level Security (RLS) on all tables

### Reporting Vulnerabilities

Found a security issue? Please report responsibly:

1. **DO NOT** create public GitHub issues for security vulnerabilities
2. Email: security@diu-os.org
3. Include: Description, steps to reproduce, potential impact
4. We'll respond within 48 hours

---

## 🤝 Contributing

We welcome contributions from the community! Here's how to get started:

### Development Setup

```bash
# Fork and clone
git clone https://github.com/YOUR_USERNAME/diu-docs.git
cd diu-docs

# Create branch
git checkout -b docs/your-improvement

# Make changes and submit PR
git commit -m "docs: your improvement description"
git push origin docs/your-improvement
```

### Contribution Guidelines

1. **Documentation Style**
   - Use clear, concise language
   - Include code examples where relevant
   - Follow existing formatting patterns

2. **Commit Messages**
   - Use [Conventional Commits](https://www.conventionalcommits.org/)
   - Format: `docs(scope): description`

3. **Pull Requests**
   - Link related issues
   - Describe changes clearly
   - Request review from maintainers

### Areas We Need Help

- [ ] Tutorials for new features
- [ ] API documentation improvements
- [ ] Translations (Russian, Chinese, Spanish)
- [ ] Architecture diagrams
- [ ] Video tutorials

---

## 📜 License

This documentation is licensed under [MIT License](LICENSE).

DIU OS codebase follows a dual licensing model:
- **Community Edition**: MIT/Apache 2.0
- **Enterprise Edition**: Proprietary (contact enterprise@diu-os.org)

---

## 📞 Support

| Channel | Purpose | Response Time |
|---------|---------|---------------|
| [Discord](https://discord.gg/diu-os) | Community support | < 24 hours |
| [GitHub Issues](https://github.com/diu-os/diu-docs/issues) | Bug reports | < 48 hours |
| [Email](mailto:support@diu-os.org) | Business inquiries | < 72 hours |

---

<div align="center">

**Built with ❤️ by the DIU OS Community**

[Website](https://diu-os.org) · [Developer Portal](https://dev.diu-os.org) · [Discord](https://discord.gg/diu-os) · [Twitter](https://twitter.com/diu_os)

</div>
