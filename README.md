<!-- BlackRoad SEO Enhanced -->

# event uus

> Part of **[BlackRoad OS](https://blackroad.io)** — Sovereign Computing for Everyone

[![BlackRoad OS](https://img.shields.io/badge/BlackRoad-OS-ff1d6c?style=for-the-badge)](https://blackroad.io)
[![BlackRoad OS](https://img.shields.io/badge/Org-BlackRoad-OS-2979ff?style=for-the-badge)](https://github.com/BlackRoad-OS)
[![License](https://img.shields.io/badge/License-Proprietary-f5a623?style=for-the-badge)](LICENSE)

**event uus** is part of the **BlackRoad OS** ecosystem — a sovereign, distributed operating system built on edge computing, local AI, and mesh networking by **BlackRoad OS, Inc.**

## About BlackRoad OS

BlackRoad OS is a sovereign computing platform that runs AI locally on your own hardware. No cloud dependencies. No API keys. No surveillance. Built by [BlackRoad OS, Inc.](https://github.com/BlackRoad-OS-Inc), a Delaware C-Corp founded in 2025.

### Key Features
- **Local AI** — Run LLMs on Raspberry Pi, Hailo-8, and commodity hardware
- **Mesh Networking** — WireGuard VPN, NATS pub/sub, peer-to-peer communication
- **Edge Computing** — 52 TOPS of AI acceleration across a Pi fleet
- **Self-Hosted Everything** — Git, DNS, storage, CI/CD, chat — all sovereign
- **Zero Cloud Dependencies** — Your data stays on your hardware

### The BlackRoad Ecosystem
| Organization | Focus |
|---|---|
| [BlackRoad OS](https://github.com/BlackRoad-OS) | Core platform and applications |
| [BlackRoad OS, Inc.](https://github.com/BlackRoad-OS-Inc) | Corporate and enterprise |
| [BlackRoad AI](https://github.com/BlackRoad-AI) | Artificial intelligence and ML |
| [BlackRoad Hardware](https://github.com/BlackRoad-Hardware) | Edge hardware and IoT |
| [BlackRoad Security](https://github.com/BlackRoad-Security) | Cybersecurity and auditing |
| [BlackRoad Quantum](https://github.com/BlackRoad-Quantum) | Quantum computing research |
| [BlackRoad Agents](https://github.com/BlackRoad-Agents) | Autonomous AI agents |
| [BlackRoad Network](https://github.com/BlackRoad-Network) | Mesh and distributed networking |
| [BlackRoad Education](https://github.com/BlackRoad-Education) | Learning and tutoring platforms |
| [BlackRoad Labs](https://github.com/BlackRoad-Labs) | Research and experiments |
| [BlackRoad Cloud](https://github.com/BlackRoad-Cloud) | Self-hosted cloud infrastructure |
| [BlackRoad Forge](https://github.com/BlackRoad-Forge) | Developer tools and utilities |

### Links
- **Website**: [blackroad.io](https://blackroad.io)
- **Documentation**: [docs.blackroad.io](https://docs.blackroad.io)
- **Chat**: [chat.blackroad.io](https://chat.blackroad.io)
- **Search**: [search.blackroad.io](https://search.blackroad.io)

---


**Pub/sub messaging for distributed systems**

## Features

- **Topics**: Create and manage event topics
- **Subscriptions**: Push and pull delivery
- **Ordering**: FIFO guarantees per partition
- **Durability**: At-least-once delivery
- **Dead Letter**: Failed message handling

## Quick Start

```typescript
import { EventBus } from '@blackroad-os/event-bus';

const bus = new EventBus({ url: 'https://events.blackroad.io' });

// Publish event
await bus.publish('agent.task.completed', {
  agentId: 'cecilia',
  taskId: 'task-123',
  result: 'success'
});

// Subscribe to events
bus.subscribe('agent.task.*', async (event) => {
  console.log('Task event:', event);
});
```

## Topics

| Topic | Description | Retention |
|-------|-------------|-----------|
| `agent.*` | Agent lifecycle events | 7 days |
| `task.*` | Task execution events | 30 days |
| `deploy.*` | Deployment events | 90 days |
| `alert.*` | System alerts | 7 days |

## Event Schema

```typescript
interface Event<T = unknown> {
  id: string;           // UUID
  type: string;         // Event type
  source: string;       // Producer ID
  time: string;         // ISO timestamp
  data: T;              // Payload
  metadata?: Record<string, string>;
}
```

## Cloudflare Queues Integration

```toml
# wrangler.toml
[[queues.producers]]
queue = "blackroad-events"
binding = "EVENTS"

[[queues.consumers]]
queue = "blackroad-events"
max_batch_size = 10
max_batch_timeout = 30
```

## Patterns

### Fan-out
```typescript
await bus.publish('order.created', order, {
  fanout: ['inventory', 'billing', 'notification']
});
```

### Request-Reply
```typescript
const response = await bus.request('agent.query', {
  query: 'status',
  timeout: 5000
});
```

---

*BlackRoad OS - Event-Driven Architecture*
