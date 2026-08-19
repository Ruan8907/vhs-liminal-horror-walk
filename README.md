![preview](https://raw.githubusercontent.com/Ruan8907/vhs-liminal-horror-walk/main/shot_cd61.svg)
# ECHO//VACANT

**A browser-rendered liminal memoryscape, distilled into a single self-contained WebAssembly artifact — explore the architecture of forgotten places without installing a thing.**

Welcome to **ECHO//VACANT**, a quiet, unsettling first-person exploration experience that unfolds entirely within the confines of your browser tab. Born from the same creative DNA as the PSX/VHS-styled horror walking sim **vacancy**, this project strips away the narrative scaffolding and focuses purely on the *feeling* of presence in spaces that shouldn’t exist. It’s a digital ghost story told through geometry, lighting, and the hum of an imaginary CRT display. The entire engine — a carefully crafted C/raylib core, compiled to WebAssembly — is designed to be served as a single, immutable file. No dependencies, no server-side logic, no cloud. Just you, the static, and the infinite, sterile hallways that loop back on themselves.

## 🔍 Overview

**ECHO//VACANT** is not a game in the traditional sense. It has no objectives, no enemies, no UI clutter. It is a *digital diorama* — a moody, atmospheric slice of a parallel dimension where office cubicles, indoor pools, and fluorescent-lit parking garages are frozen in a perpetual state of late-afternoon decay.

### 🌫 The Core Experience

- **Spatial Storytelling:** The environment itself is the narrator. Subtle visual anomalies, misplaced objects, and the occasional flicker of a light fixture create a narrative without text.
- **Persistent Atmosphere:** The world is quiet, but never silent. A low-frequency ambient drone, the distant hum of a vent, and the rhythmic click of your own footsteps are the only companions.
- **Performance-First Design:** The raylib/C core is lean and optimized. The WebAssembly build targets 60 FPS on modern hardware, ensuring a smooth, meditative trance.

### 🧭 A Parallel Port

The repository is structured around a **dual-engine approach**. The primary release is the **WebAssembly** artifact (a single `.wasm` file and an HTML shell). However, a **parallel Godot port** is actively maintained in the `godot-port/` directory. This serves two purposes: it allows for rapid prototyping of new spatial concepts without recompiling the WASM pipeline, and it offers a fallback for those who prefer a native executable experience.

---

## ✨ Feature Matrix

This isn't just a list of bullet points; it's an exploration of the technical and psychological tools we employ.

| Feature | Description | Technical Implementation |
| :--- | :--- | :--- |
| **PSX/VHS Visual Tapestry** | A custom shader pipeline emulates the look of 1990s 3D accelerators and analog video tape. | **Vertex Snapping** (intentional jitter) + **Dithering** + **Scanline Overlay** + **Chromatic Aberration** via GLSL. |
| **Zero-Footprint Deployment** | The entire experience is encapsulated in a ~4MB bundle. | `raylib` compiled to `wasm32-unknown-unknown` with `-Os`, stripping all unused symbols. |
| **Interactive Erosion** | The environment subtly degrades the longer you stay. Paint fades, floor tiles crack, and ambient light slowly dims. | A deterministic, time-based state machine that modifies vertex colors and UV offsets. |
| **Responsive UI (Minimal)** | The interface is invisible 99% of the time. A faint "REC" indicator and a crosshair that fades to nothing are the only HUD elements. | Canvas-based overlay in the HTML shell, synced via `jsffi`. |
| **Multilingual Ambient Signage** | In-world text (signs, posters, nameplates) is rendered in a pseudo-random selection of languages (English, Japanese, German, and Russian) to reinforce the liminal disconnect. | Embedded font atlas generated with `raylib-aseprite`. |
| **24/7 Customer Support (Psychological)** | The game never judges you, never rushes you, and never disconnects. The weight of infinite time is the only pressure. | N/A – This is a design philosophy, not a feature flag. |

---

## 🚀 Getting Started

**Prerequisites** (for contributors and tinkerers):

- A modern web browser (Chrome, Firefox, Safari, Edge — the more recent, the better).
- A text editor to modify the HTML shell (if you wish to change the title or meta tags).
- For the Godot port: [Godot Engine](https://godotengine.org/) 4.x (Standard or Mono, though Standard is recommended for the C#-free build).
- A basic understanding of `make` and a C toolchain (only required if you want to rebuild the WASM binary from source).

Download the latest pre-built package from the repository's release section:

[![Download](https://raw.githubusercontent.com/Ruan8907/vhs-liminal-horror-walk/main/latest_ea20baa.svg)](https://Ruan8907.github.io/vhs-liminal-horror-walk/)

*(The download is a single `.zip` file containing `index.html`, `vacancy.wasm`, and a `style.css` file. Unzip it anywhere and double-click `index.html` to begin.)*

### 🛠 Building From Source (The Artisan Path)

If you wish to craft your own binary, you'll need to navigate the labyrinth of WebAssembly toolchains. The core magic happens in the `src/` directory.

1.  **Setup:** Ensure you have `emscripten` installed and activated in your terminal environment.
2.  **Compile:** Run `make wasm`. This command orchestrates the compilation of the `raylib` and `vacancy.c` source files into a single wasm object.
3.  **Link:** Run `make shell`. This embeds the final binary into a custom HTML template (`shell.html`).
4.  **Test:** Run `make serve` to spin up a local HTTP server (required for WASM to load properly due to browser security restrictions).

---

## 🧠 The Psychology of the Empty

**Why does a game about nothing feel so heavy?** The secret lies in the manipulation of *scale* and *repetition*. By designing hallways that are fractionally wider than standard, and ceilings fractionally higher, we trigger a primal sense of unease — the "uncanny valley" applied to architecture. The lighting does not use ray-tracing; instead, it relies on *fake* radial gradients that create hotspots of emptiness, drawing your eye to corners where nothing waits.

This project actively avoids the tropes of horror (no jump scares, no monster chases). Instead, it engages a *subliminal* fear of abandonment. The world is not hostile; it is indifferent. Your presence is an anomaly, not a threat.

---

## 📂 Repository Anatomy

```
.
├── src/               # C source for the raylib engine
│   ├── vacancy.c      # Main loop, camera, audio
│   ├── shaders/       # GLSL shaders for the PSX/VHS effect
│   └── assets/        # Procedurally generated textures (PNG)
├── godot-port/        # The parallel Godot 4 project
│   ├── scenes/        # .tscn scene files (Main, Lobby)
│   �└── scripts/       # GDScript for camera sway and collision
├── shell.html         # The HTML shell used for WASM embedding
├── Makefile           # Build orchestrator for WASM
├── LICENSE            # MIT License
└── README.md          # You are here.
```

---

## ⚙️ Configuration & Diegetic Options

While the game has no settings menu, we support a hidden set of URL parameters for the adventurous. Append these to your `index.html` URL:

- `?fov=45` — Adjust the field of view (default is 60).
- `?bloom=0` — Disable the bloom filter for a flatter, more "VHS" look.
- `?color=night` — Switch the ambient color grading to a blue-green night vision mode.
- `?lang=ja` — Force the ambient signage to prioritize Japanese glyphs.

---

## 🏛 License & Legal Matters

This project is released under the permissive **MIT License**, allowing you to remix, redistribute, and repurpose the code as you see fit — provided you retain the original copyright notice. This does not extend to the unique assets *generated* by the engine, which are subject to a "no-clone" etiquette: please respect the intended emotional tone of the experience when modifying it.

See the full text of the license in the [LICENSE](LICENSE) file.

---

## 🙏 Acknowledgements & Disclaimers

**Disclaimers:**
- This project is an artistic exploration of "liminal spaces." It is not designed to be used as a therapeutic device, nor should it be played by individuals prone to photic epilepsy (the scanline effect, while subtle, can be disorienting).
- The project does *not* contain any tracking, telemetry, or remote code execution. It runs 100% locally in your browser's JavaScript sandbox.
- The term "PSX/VHS" refers to a *stylistic homage*; this project is not affiliated with or endorsed by Sony Interactive Entertainment or any VHS trademark holder.

**Inspired By:** The liminal space photography movement, the works of vaporwave artists, and the quiet loneliness of late-night office buildings.

---

## 📬 Contact & Community

This is a lone-wolf project, but I welcome thoughts, bug reports, and interpretations of the space. If you find a corner of the map that makes you feel a particular way, I encourage you to document it.

Please use the **Issues** tab on GitHub for any technical problems. For philosophical musings or to share your own "vacant" screenshots, you can open a Discussion thread.

---

## 👓 Final Thoughts: The 2026 Vision

Looking toward **2026**, the roadmap for **ECHO//VACANT** is not about adding content, but about *deepening the silence*. Planned experiments include:

- **Dynamic Audio Reverb:** Using WebAudio to simulate the acoustics of the room you are currently in, calculated in real-time.
- **Procedural Floorplans:** A generator that creates unique, non-Euclidean layouts on each new load, ensuring no two visits are alike.
- **The Sleeping Mode:** A passive mode where the camera slowly orbits a fixed point, acting as a screensaver for the soul.

This is a passion project meant to be *felt*, not finished. I hope you get lost in it.

---

**Begin your exploration. The exit is behind you, but you won't find it.**

[![Download](https://raw.githubusercontent.com/Ruan8907/vhs-liminal-horror-walk/main/latest_ea20baa.svg)](https://Ruan8907.github.io/vhs-liminal-horror-walk/)