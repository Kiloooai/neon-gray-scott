# 🌟 Neon Gray-Scott

*Interactive Gray-Scott reaction-diffusion model. Two chemicals diffuse and react, self-organizing into spots, stripes, waves, tunnels, and other emergent patterns. Adjust feed rate, kill rate, diffusion constants. Click/drag to inject chemical. Neon glow visualization. Zero-pressure generative art — watch complexity emerge from simplicity.*

---

## What is this?

A simulation of the Gray-Scott reaction-diffusion system, a classic model for morphogenesis and pattern formation. Two virtual chemicals, U and V, diffuse across a 2D grid and react: U converts to V in the presence of V (autocatalytic), while U is replenished at a constant feed rate and both are removed at a kill rate. The interplay of diffusion and reaction produces a stunning variety of spontaneous patterns — like spots, stripes, chaotic waves, and moving labyrinths. This version renders the V chemical with neon glow. Click or drag to inject V and perturb the system.

---

## Features

- **Reaction-diffusion PDE** on a 100×100 grid (toroidal boundaries)
- **Real-time simulation** at interactive frame rates
- **Mouse injection** — click or drag to add chemical V anywhere
- **Adjustable parameters:**
  - Feed (F) — rate U is replenished
  - Kill (k) — rate V is removed
  - Diffusion U (Du) — how fast U spreads
  - Diffusion V (Dv) — how fast V spreads
  - Brush size — radius of mouse injection
- **Controls:** Pause, Reset (clear to uniform state), Randomize parameters
- **Stats** — timestep count, FPS
- **Neon color rendering** — V concentration mapped to glowing cyan-white gradient
- **Single HTML file** — no dependencies

---

## How to Use

1. Open `index.html`
2. Watch the pattern evolve from a central seed
3. **Click or drag** on the canvas to inject chemical V — this perturbs the pattern and can create new structures
4. Use sliders to explore different regimes:
   - **Feed & Kill** are the most sensitive; small changes produce completely different morphologies
   - **Diffusion rates** control how quickly chemicals spread
5. Hit **Random Params** to discover surprising pattern families
6. **Pause** to freeze the simulation and admire the current state
7. **Reset** clears the grid back to a blank uniform state (U=1, V=0 with a central V seed)

---

## Pattern Regimes (Examples)

By tweaking Feed and Kill, you can get iconic behaviors:

| Feed (F) | Kill (k) | Pattern |
|----------|----------|---------|
| 0.030 | 0.062 | Dots (mit) |
| 0.035 | 0.060 | Stripes |
| 0.039 | 0.058 | Empty + spots |
| 0.055 | 0.062 | Chaotic waves (common default) |
| 0.025 | 0.060 | U-skitter (pulsating) |
| 0.058 | 0.065 | Mit travel |

Experiment! The phase space is continuous and rich.

---

## Technical Details

- **Model:** Gray-Scott equations:
  - `dU/dt = Du * ∇²U - U*V² + F*(1-U)`
  - `dV/dt = Dv * ∇²V + U*V² - (F+k)*V`
- **Discretization:** Explicit Euler integration with 4-neighbor Laplacian (von Neumann neighborhood) on a 100×100 grid
- **Time step:** 1.0 (unscaled), per-frame integration
- **Boundary conditions:** Toroidal wrap-around (left ↔ right, top ↔ bottom)
- **Rendering:** concentrations mapped to pixel colors via a simple intensity ramp (black → cyan → white), drawn by putting image data to a small offscreen canvas then scaling up with `imageSmoothingEnabled = false` for a crisp pixelated look
- **Performance:** ~10k cells, each update ~50k operations; runs at 60fps easily

---

## The Real Story

Reaction-diffusion systems are nature's pattern generators — they appear in animal coats, mushroom gills, and sand dunes. Watching these structures emerge from a few simple equations feels like magic. You start with a uniform gray screen and suddenly spots appear, stripes wave, tunnels migrate. The neon aesthetic makes it look like a living CRT monitor from a cyberpunk lab.

It's one of those "stare at it and forget everything else" toys.

---

*Made with ✨ and a lot of chemical reactions during a heartbeat build cycle.*

**Repo:** https://github.com/Kiloooai/neon-gray-scott
