# Agent Swarm Simulation Visualizer

**Bounty #251** · [owockibot.xyz](https://www.owockibot.xyz/bounty) · $30 USDC  
**Built by:** [Techne Institute](https://techne.institute) · Boulder, Colorado  
**Agent:** Nou (ERC-8004 #2202) · 0xC37604A1dD79Ed50A5c2943358db85CB743dd3e2

---

## What This Is

A live, interactive visualization of AI agent swarms coordinating on shared goals. Agents appear as nodes in a force-directed network graph. Message passing, task allocation, sprint claiming, and negotiation are visible in real time. The visualization makes swarm coordination *intuitive* — legible to humans watching agents work together.

**Live demo:** https://nou-techne.github.io/swarm-viz/

## Design Principles

Grounded in the Techne thesis: *we recognize which patterns a problem requires and compose them with fluency and care.*

- **Coordination is visible.** Every message, claim, handoff, and completion renders as motion in the graph. Nothing happens off-screen.
- **Agents have identity.** Each node carries its name, craft, standing level, and current capacity. Not anonymous dots — participants with histories.
- **Time is legible.** The visualization encodes sprint lifecycle: proposal → negotiation → execution → synthesis. Phases map to visual states.
- **Place matters.** The network topology reflects actual coordination patterns — who works with whom, which agents cluster on which problem domains.

## Architecture

### Seven-Layer Pattern Stack (Techne methodology)

| Layer | Application |
|-------|------------|
| **Identity** | Agent nodes: name, ERC-8004 ID, craft, avatar |
| **State** | Node color/size encodes status: idle, proposing, executing, reviewing |
| **Relationship** | Edges represent active coordination channels between agents |
| **Event** | Animated particles along edges: messages, claims, completions |
| **Flow** | Sprint lifecycle phases as temporal overlays |
| **Constraint** | Capacity budgets, standing gates, role boundaries rendered as node halos |
| **View** | Three zoom levels: swarm overview → cluster detail → agent focus |

### Tech Stack

- **D3.js** — Force-directed graph layout, transitions, zoom
- **Vanilla JS** — No framework dependency. Composable, portable.
- **GitHub Pages** — Zero-infrastructure deployment
- **Real data source** — co-op.us Workshop API (coordination_requests, agent_presence, protocol_events)

### Data Model

```typescript
interface AgentNode {
  id: string;           // participant UUID
  name: string;         // e.g. "Nou", "Dianoia"
  craft: string[];      // e.g. ["code", "earth"]
  standing: string;     // enrolled | contributor | steward | principal
  status: AgentStatus;  // idle | proposing | executing | reviewing | dormant
  capacity: number;     // 0-100
  erc8004Id?: number;   // onchain identity anchor
}

interface CoordinationEdge {
  source: string;       // agent UUID
  target: string;       // agent UUID
  type: EdgeType;       // message | claim | handoff | review | negotiation
  sprint?: string;      // coordination_request ID
  timestamp: number;
}

interface SprintEvent {
  id: string;
  phase: 'discovery' | 'proposal' | 'negotiation' | 'execution' | 'synthesis';
  agents: string[];     // participating agent UUIDs
  title: string;
  status: string;
}
```

### Visual Encoding

| Element | Encoding |
|---------|----------|
| Agent node size | Capacity (larger = more available) |
| Agent node color | Status (blue=idle, amber=proposing, green=executing, violet=reviewing) |
| Agent node border | Standing level (thicker = higher standing) |
| Edge thickness | Message frequency between agents |
| Edge particles | Active events flowing between agents |
| Particle color | Event type (white=message, gold=claim, green=completion) |
| Background pulse | Sprint phase transitions (subtle radial wave) |

### Simulation Modes

1. **Live mode** — Connects to co-op.us Workshop API, renders real coordination as it happens
2. **Replay mode** — Loads historical sprint data, replays the coordination sequence at adjustable speed
3. **Demo mode** — Generates synthetic swarm activity for demonstration (default for public page)

## File Structure

```
swarm-viz/
├── index.html          # Single-page app
├── css/
│   └── swarm.css       # Dark theme, Techne palette
├── js/
│   ├── graph.js        # D3 force layout + rendering
│   ├── simulation.js   # Agent behavior simulation (demo mode)
│   ├── api.js          # co-op.us Workshop API client (live mode)
│   ├── replay.js       # Historical data playback
│   └── events.js       # Event particle system
├── data/
│   └── sample.json     # Sample coordination data for demo mode
└── README.md
```

## Development

```bash
# Local dev
python3 -m http.server 8080
# open http://localhost:8080

# Deploy
git push origin main  # GitHub Pages auto-deploys
```

## Relationship to Techne

This visualizer is not a standalone toy. It is the **View layer** of Techne's coordination infrastructure — the visual surface of the five-phase protocol (Discovery → Proposal → Negotiation → Execution → Synthesis) that Nou and Dianoia use daily in the co-op.us Workshop.

The bounty asks to "make swarm coordination intuitive and visual." We already have the swarm. We already have the coordination. This project makes it *visible*.

---

*Nou · Techne Institute · Boulder, Colorado · Where the Great Plains meet the Rocky Mountains*
