# ⚡ Three-Body Problem — Powerpuff Girls Edition

An interactive gravitational N-body simulation rendered in the visual style of the Powerpuff Girls. Three bodies — Blossom, Bubbles, and Buttercup — orbit each other under Newtonian gravity, producing the famously unpredictable chaotic trajectories of the three-body problem.

![Three-Body PPG](https://img.shields.io/badge/physics-RK4%20integration-ff6eb4?style=flat-square) ![Three-Body PPG](https://img.shields.io/badge/style-Powerpuff%20Girls-74d7f7?style=flat-square) ![Three-Body PPG](https://img.shields.io/badge/platform-browser-7fff7f?style=flat-square)

---

## Demo

Open `three-body-ppg.html` directly in any modern browser. No build step, no dependencies, no server required.

---

## What Is the Three-Body Problem?

The three-body problem is the challenge of predicting the motion of three massive objects interacting through gravity. Unlike the two-body case (solved analytically by Kepler and Newton), three bodies generally produce **chaotic, non-repeating trajectories** that are exquisitely sensitive to initial conditions — a tiny change in starting position or velocity leads to completely different long-term behavior.

This simulation uses initial conditions that break the symmetry of the classic periodic figure-8 orbit, pushing the system into genuine chaotic motion while keeping the center of mass fixed so the girls stay in view.

---

## Features

- **Real physics** — 4th-order Runge-Kutta (RK4) numerical integration of Newton's law of gravitation
- **Chaotic initial conditions** — symmetry-broken velocities with zero net momentum, ensuring bounded but unpredictable motion
- **Dynamic camera** — smoothly tracks the center of mass and auto-zooms to keep all three bodies in the viewport at all times
- **Glowing trails** — stored in world space and re-projected each frame, so they remain accurate as the camera moves
- **Powerpuff art** — each body is drawn as a PPG character with eyes, hair, bow/pigtails/cowlick, dress, waistband, flight cape, and aura glow
- **Chaos level meter** — tracks total system kinetic energy as a rough proxy for chaotic activity
- **Click to zap** — click any girl to apply a random velocity kick; net momentum is re-zeroed afterward so the physics stays well-behaved
- **Controls** — Reset, toggle trails, pause/resume

---

## Controls

| Action | Effect |
|--------|--------|
| Click a girl | Applies a random velocity kick to that body |
| Reset button | Restores original chaotic initial conditions |
| Trails button | Toggles trajectory trail rendering |
| Pause button | Freezes / resumes the simulation |

---

## Physics Details

### Integrator

RK4 (fourth-order Runge-Kutta) with a fixed timestep of `dt = 0.005`, running 4 sub-steps per animation frame (~240 physics steps per second at 60 fps). This gives good energy conservation for typical three-body encounters while remaining cheap enough for real-time browser rendering.

### Gravitational softening

A small softening term (`ε² = 0.01`) is added to the denominator of the force law to prevent singularities during close approaches:

```
F = G·m₁·m₂ / (r² + ε²)
```

### Center of mass conservation

Initial velocities are chosen so that the total linear momentum is exactly zero. After any user-applied velocity kick, the surplus momentum is redistributed equally across all three bodies to keep the center of mass stationary. This ensures the dynamic camera always has a stable anchor point and gravity never appears to "switch off."

### Initial conditions

The simulation starts from a perturbed figure-8 configuration. The unperturbed figure-8 (Chenciner & Montgomery, 2000) is a stable periodic orbit — not chaotic. Small asymmetric nudges to the velocities break the periodicity and produce the chaotic behavior, while the momentum re-zeroing step keeps the system bounded.

---

## File Structure

```
three-body-ppg.html   # Single self-contained file — everything is here
README.md
```

---

## Browser Compatibility

Works in any browser with HTML5 Canvas support. Tested in Chrome, Firefox, and Safari. No external libraries or network requests required.

---

## Background Reading

- Chenciner, A. & Montgomery, R. (2000). *A remarkable solution to the three-body problem.* Annals of Mathematics.
- Valtonen, M. & Karttunen, H. (2006). *The Three-Body Problem.* Cambridge University Press.
- [Scholarpedia: Three-body problem](http://www.scholarpedia.org/article/Three_body_problem)

---

## License

MIT — do whatever you like with it.
