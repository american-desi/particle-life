# Particle Life - Emergent Artificial Life Simulation

A real-time simulation of artificial life where thousands of particles interact according to simple rules, producing complex emergent behaviors reminiscent of biological systems.

## How to Run

Open `index.html` in any modern web browser. No build tools, server, or dependencies required.

```bash
open index.html
# or
python3 -m http.server 8000   # then visit http://localhost:8000
```

## What You Are Seeing

Colored particles represent different "species." Each species has an attraction or repulsion value toward every other species, stored in an **interaction matrix**. These values are randomly generated and range from -1 (strong repulsion) to +1 (strong attraction).

Despite having no explicit programming for complex behavior, the particles self-organize into structures that resemble:

- **Cells** -- clusters with a membrane-like boundary
- **Hunting** -- one species chasing another while fleeing a third
- **Flocking** -- groups moving coherently in the same direction
- **Symbiosis** -- two species orbiting or co-existing in stable formations
- **Mitosis-like splitting** -- clusters that grow and divide

## The Science

### Particle Life as a Model

Particle Life belongs to a family of artificial life simulations inspired by work on **primordial particle systems** and **Lenia**. The core idea comes from complexity science: simple local rules applied uniformly can produce globally complex, life-like behavior without any central coordination.

### How the Physics Works

1. **Force function**: A piecewise linear function that is repulsive at very short range (preventing particles from collapsing onto each other) and attractive or repulsive at medium range (governed by the interaction matrix).

2. **Interaction matrix**: An NxN table where entry (i, j) determines how species i responds to species j. Positive values mean attraction; negative values mean repulsion. Randomizing this matrix produces wildly different emergent behaviors.

3. **Friction**: A velocity damping factor that prevents particles from accelerating indefinitely, keeping the system stable.

4. **Toroidal boundary**: The simulation wraps around at the edges, so particles leaving one side reappear on the opposite side. This eliminates edge effects.

### Why It Looks Alive

The emergent behavior arises because:
- **Short-range repulsion** prevents collapse, acting like physical volume
- **Medium-range attraction/repulsion** creates the equivalent of chemical bonds
- **Asymmetric interactions** (species A attracts B, but B repels A) create pursuit and evasion dynamics
- **Multiple species** create ecological niches and food-chain-like dynamics

This is related to the concept of **dissipative structures** (Ilya Prigogine) -- systems far from thermodynamic equilibrium that maintain organized states through continuous energy flow.

## Controls

| Control | Description |
|---------|-------------|
| **Particles** | Total number of particles (500-6000) |
| **Species** | Number of distinct species (3-10) |
| **Interact Radius** | How far particles can sense each other |
| **Friction** | Velocity damping (higher = more viscous) |
| **Force Strength** | Global multiplier on all forces |
| **Trail Length** | How quickly trails fade (lower = longer trails) |
| **Time Step** | Simulation speed |

### Preset Buttons

- **Randomize Rules** -- generates a fully random interaction matrix
- **Symmetric** -- generates a matrix where A's effect on B equals B's effect on A (produces crystal-like structures)
- **Chains** -- each species strongly attracts the next in a cycle (produces spiraling chains)
- **Hunters** -- each species hunts the next and flees the previous (produces predator-prey dynamics)

### Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `Space` | Pause / Resume |
| `R` | Randomize rules |
| `H` | Hide / Show control panel |

### Mouse Controls

- **Drag** to pan the view
- **Scroll** to zoom in/out

## Performance

The simulation uses **spatial hashing** to achieve approximately O(n) performance per frame instead of the naive O(n^2) approach. Each particle only checks interactions with particles in neighboring grid cells, making it feasible to simulate thousands of particles at 60 FPS.

## Credits

Inspired by Jeffrey Ventrella's Clusters, Tom Mohr's Particle Life, and the broader artificial life research community.

## License

Public domain. Use freely for any purpose.
