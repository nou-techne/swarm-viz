# Build: Agent Swarm Simulation Visualizer

Build a single `index.html` file that is a live, interactive D3.js force-directed graph visualization of AI agent swarm coordination.

## Design System

Use EXACTLY the same design system as `reference-design.html` in this repo:
- Same CSS variables (--bg, --surface, --primary, --nou-color, --dia-color, etc.)
- Same fonts (Cormorant display, Source Serif 4 body, IBM Plex Mono)
- Same component patterns (eyebrow, section-label, stat-grid, agent-card, etc.)
- Dark theme forced, no light mode
- Same responsive breakpoints

## Structure

The page has these sections in order:

### 1. Header
- Eyebrow: owockibot.xyz · Bounty #251 · Live Workshop · Bounty #249
- Title: "Swarm —" then italic "Agent Coordination" then "Visualized"
- Subtitle: "Real coordination between AI agents, rendered as a living graph. Every message, claim, and completion visible as motion. Data source: the co-op.us Workshop."
- Meta bar: Mode (Demo/Live/Replay toggle), Agents (count), Sprints active, Dimensions (7 · e/H-LAM/T+S)

### 2. The Visualization (MAIN FEATURE)
A large (full-width, ~600px tall) SVG canvas with a D3 force-directed graph.

**Agent Nodes:**
- Circles sized by capacity (40-80px diameter)
- Colored by status: blue (#7a9ab5) = idle, amber (#c4956a) = proposing, green (#8aba8a) = executing, violet (#9a7ab5) = reviewing
- Border thickness = standing level (enrolled=1px, contributor=2px, steward=3px, principal=4px)
- Inner text: agent initials (monospace)
- Outer label: agent name (Cormorant font)
- Subtle glow animation when active

**Edges (Coordination Links):**
- Lines between agents who are coordinating
- Colored by work level: white = A-work, amber = B-work, rose (#b57a7a) = C-work
- Animated particles (small dots) flowing along edges when events happen
- Thickness = message frequency

**Sprint Artifacts:**
- Small rectangles orbiting near the executing agent
- Show sprint title (truncated), layer badges as tiny colored dots
- Layer badge colors: Identity=indigo, State=emerald, Relationship=amber, Event=rose, Flow=cyan, Constraint=slate, View=violet

**Environment Layer:**
- Background gradient shifts based on solar phase (dark=night, warm tint=dawn/dusk, neutral=day)
- Subtle lunar phase indicator in corner (text, not image)
- Roadmap block progress arc at top of canvas

**Controls overlay (top-right of canvas, semi-transparent):**
- Dimension toggles: H L A M T e S keys (small badges showing which are active)
- Work level toggles: A B C
- Mode: Demo | Live | Replay

### 3. e/H-LAM/T+S Framework Section
Use the intro-block pattern from reference-design.
Left: prose explaining Engelbart's framework and Techne's modification
Right: stat-grid showing the 7 dimensions with their meanings

Then a table showing each dimension, what it means, and how it maps to the visualization layer.

### 4. A/B/C Work Levels Section
Three cards (like agent-cards) side by side:
- A-work card: "Doing" — foreground particles, fast motion, white/gold
- B-work card: "Improving" — structural evolution, amber edges
- C-work card: "The Bootstrap" — outermost ring, roadmap progression, rose

### 5. Seven-Layer Pattern Stack
Table (arch-table style) showing: Layer | Color | Sprint Example | Visual Encoding

### 6. Simulation Data
In Demo mode, generate synthetic but realistic agent behavior:
- 4-6 agents: Nou, Dianoia, plus 2-4 synthetic agents with names like "Arete", "Kairos", "Praxis", "Ergon"
- Agents periodically send heartbeats (particle from agent to center)
- Sprints get proposed (new edge + artifact), claimed (edge animates), completed (burst)
- Every 8-10 seconds, a new event happens
- Sprint titles should be realistic: "Patronage Event Types", "Standing Gate Constraints", "Watershed Data Pipeline", "Contribution Rarity Algorithm"

### 7. Lineage Section
Three cards linking to prior bounties: #237 Watershed, #249 A2A Protocol, and this one.

### 8. Footer
Same pattern as reference-design. Techne Institute branding, links, copyright line.

## Technical Requirements
- Single index.html file, all CSS and JS inline
- D3.js v7 loaded from CDN (d3js.org)
- No other external dependencies except fonts
- Smooth 60fps animations using requestAnimationFrame for particles
- Force simulation: d3.forceSimulation with forceLink, forceManyBody, forceCenter, forceCollide
- Canvas should be responsive (resize on window resize)
- Demo mode starts automatically on load

## Critical: Get the Design Right
Study reference-design.html carefully. Match:
- The warm amber (#c4956a) primary color
- The muted (#777777) secondary text
- The surface (#141414) card backgrounds
- The Cormorant headings style
- The IBM Plex Mono labels style
- The spacing rhythm (48px sections, 24px card padding)
- The subtle border (1px solid #2a2a2a) style

The visualization should feel like it belongs on the same site as reference-design.html.
