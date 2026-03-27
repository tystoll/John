# 🎱 Pool Trainer — John's Pool Hall

> An augmented reality pool coaching system that projects real-time shot guidance directly onto the table surface using overhead camera tracking and a ceiling-mounted projector.

---

## Overview

Pool Trainer transforms a standard pool table into an interactive coaching experience. A camera mounted above the table tracks the player's cue stick alignment in real time. A projector then overlays visual shot guidance directly onto the felt — showing the cue ball's intended path, the contact point, and the deflection angle after impact.

Inspired by the aim-assist and trajectory systems from classic browser pool games (Yahoo Pool), brought into the physical world.

---

## How It Works

```
         [ Camera ]  [ Projector ]
               ↓          ↓
         ┌─────────────────────────┐
         │                         │
         │    ●  ← Cue Ball        │
         │    │                    │
         │    │  (trajectory line) │
         │    ↓                    │
         │    ○  ← Contact Point   │
         │   / \                   │
         │  /   \ (deflect paths)  │
         │ ↙     ↘                 │
         └─────────────────────────┘
                Pool Table
```

**Step-by-step flow:**

1. **Player approaches the table** — the overhead camera detects the cue stick entering the frame.
2. **Cue stick alignment is tracked** — computer vision calculates the stick's angle and direction vector in real time.
3. **Trajectory is computed** — the system calculates the cue ball's intended path based on current stick alignment.
4. **Contact point & deflection are resolved** — for a single contact event, the system determines where the cue ball will strike a target ball and projects both the cue ball's post-impact path and the target ball's deflection direction.
5. **Projector overlays the guidance** — lines, indicators, and the ghost ball position are projected directly onto the felt surface.
6. **Player adjusts and shoots** — the projection updates in real time as the player moves their stick.

---

## Projection Overlay Elements

| Element | Description |
|---|---|
| **Trajectory Line** | Dotted or solid line from cue ball along the stick's aim vector |
| **Ghost Ball** | Semi-transparent circle showing where the cue ball will be at contact |
| **Contact Point Indicator** | Highlight on the target ball at the point of impact |
| **Cue Ball Deflection Path** | Line showing cue ball direction after impact |
| **Target Ball Path** | Line showing where the target ball will travel post-contact |

> Scope: Single contact point only (no multi-ball chain reactions in v1).

---

## Hardware Setup

| Component | Role |
|---|---|
| Overhead Camera | Captures top-down view of the entire table; feeds frames to CV pipeline |
| Ceiling-Mounted Projector | Projects trajectory overlay onto the table surface |
| Processing Unit (PC/NUC) | Runs tracking, physics calculation, and projection rendering |
| Table | Standard 7ft, 8ft, or 9ft pool table (calibration required per table size) |

### Camera Placement

- Mounted directly above the center of the table
- Must cover the full table surface in a single frame
- Recommended: wide-angle lens, minimum 1080p @ 60fps

### Projector Placement

- Mounted at the same overhead position or offset slightly
- Must be calibrated to map projected pixels to physical table coordinates (homography matrix)
- Keystone correction recommended for off-center mounts

---

## Software Architecture

```
┌──────────────────────────────────────────────┐
│                  Pool Trainer                │
│                                              │
│  ┌─────────────┐     ┌─────────────────────┐ │
│  │  CV Module  │────▶│  Physics / Geometry │ │
│  │  (camera    │     │  Engine             │ │
│  │   tracking) │     │  (trajectories,     │ │
│  └─────────────┘     │   deflection)       │ │
│                      └────────┬────────────┘ │
│                               │              │
│                      ┌────────▼────────────┐ │
│                      │  Projection Render  │ │
│                      │  (overlay output)   │ │
│                      └─────────────────────┘ │
└──────────────────────────────────────────────┘
```

### Key Modules

- **`camera/`** — Frame capture, perspective correction, table boundary detection
- **`tracking/`** — Cue stick detection, angle extraction, alignment vector calculation
- **`physics/`** — Ball contact geometry, deflection angle math (cut angle, throw, squirt)
- **`projection/`** — Overlay rendering, homography mapping, real-time display output
- **`calibration/`** — Camera-to-projector alignment tool, table corner registration

---

## Calibration

Before first use, the system must be calibrated to the specific table and room:

1. **Table registration** — Mark the four corner pockets; the system builds a homography matrix to map camera pixels → table coordinates → projector pixels.
2. **Camera distortion correction** — Run the lens calibration utility with a checkerboard pattern.
3. **Projector alignment** — Confirm the projected overlay lands exactly on physical table coordinates.
4. **Ball detection tuning** — Adjust HSV thresholds for the specific felt color and ball set.

---

## Getting Started

```bash
# Clone the repo
git clone https://github.com/johns-pool-hall/pool-trainer.git
cd pool-trainer

# Install dependencies
pip install -r requirements.txt

# Run calibration
python calibrate.py

# Launch the trainer
python main.py
```

---

## Dependencies

- Python 3.10+
- OpenCV (`cv2`) — camera capture and computer vision
- NumPy — matrix math and geometry
- Pygame / OpenGL — projection rendering
- (Optional) MediaPipe — hand/stick pose estimation

---

## Roadmap

- [x] Cue stick angle tracking
- [x] Single-contact trajectory projection
- [x] Ghost ball overlay
- [ ] Spin / english effect visualization
- [ ] Multi-rail bank shot projection
- [ ] Player session stats & shot history
- [ ] Difficulty modes (beginner / advanced overlay detail)
- [ ] Integration with scoring systems

---

## Credits

Built for **John's Pool Hall**.  
Shot geometry reference adapted from offline Yahoo Pool physics documentation.

---

## License

MIT License — see `LICENSE` for details.
