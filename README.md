# 〰️ WaveLab — Interactive Mathematics of Sound

> Five interactive modules that let you **see** and **hear** the mathematics behind sound, waves, and motion — built entirely with HTML, CSS, and JavaScript. No frameworks, no build step, no dependencies.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Web Audio API](https://img.shields.io/badge/Web_Audio_API-4cc9f0?style=flat)
![Canvas 2D](https://img.shields.io/badge/Canvas_2D-b14aed?style=flat)
![No dependencies](https://img.shields.io/badge/dependencies-none-00f5d4?style=flat)

**[🚀 Live Demo →](https://lanayaberg.github.io/wavelab)**

---

## ✨ What is this?

WaveLab is a single-page interactive tool with **five modules**, each exploring a different piece of the mathematics that makes sound and periodic motion work — from basic waveforms to 3D parametric curves. Every module is fully interactive and most of them produce real audio through the Web Audio API.

It's both a **creative toy** and a **learning tool** — the kind of thing that makes an abstract formula in a textbook suddenly click.

---

## 🎛️ The Five Modules

### 〜 Waveform Lab
The foundation. Five wave types — Sine, Square, Sawtooth, Triangle, and a live Fourier approximation — rendered on an animated oscilloscope with CRT phosphor glow, alongside a Lissajous figure and a harmonic spectrum analyzer. Adjust frequency, amplitude, phase, and harmonic count; hear the result instantly.

### ◎ Fourier Epicycles
Joseph Fourier proved in 1822 that *any* periodic wave can be built from a sum of rotating circles. This module animates that proof directly: watch a chain of circles — each one a single sine term — rotate and combine to trace out a square, sawtooth, or triangle wave in real time. Add more harmonics and watch the approximation sharpen.

### ∿+∿ Wave Mixer
Two fully independent oscillators (type, frequency, amplitude) are summed point-by-point into a third wave. Set their frequencies close together and you'll hear **beating** — the audible pulsing that happens when two nearby frequencies interfere constructively and destructively over time.

### ♪ Piano
A two-octave virtual keyboard (C4–C6) playable by mouse, touch, or computer keyboard (A S D F G H J K L for white keys, W E T Y U O for black keys). Choose any of the four waveforms as the instrument's timbre and watch a live oscilloscope trace whatever note is currently playing.

### ◆ 3D Lissajous
Three independent sine oscillators drive a point through 3D space; a rotation matrix projects it onto the 2D canvas with a phosphor-trail effect. Drag to rotate the figure manually, tune the frequency ratios, and press play to hear the three oscillators as a chord.

---

## 📐 The Math Behind It

### Fourier Series
The core insight powering both the Waveform Lab and the Epicycles module: any periodic function can be expressed as an infinite sum of sines.

```
Square:    y = (4/π) Σ sin((2k−1)t)/(2k−1),      k = 1, 2, 3, ...
Sawtooth:  y = (2/π) Σ (−1)ⁿ⁺¹ sin(nt)/n,         n = 1, 2, 3, ...
Triangle:  y = (8/π²) Σ (−1)ᵏ sin((2k+1)t)/(2k+1)², k = 0, 1, 2, ...
```

This theorem underpins digital audio compression (MP3), image compression (JPEG), and signal processing generally.

### Wave Interference & Beating
When two waves of similar frequency are added, the result is a wave whose amplitude rises and falls at the *difference* between the two frequencies:

```
beat frequency = |f₁ − f₂|
```

This is why two out-of-tune guitar strings produce an audible "wah-wah" — and why piano tuners use it to tune by ear.

### Rotation Matrices (3D Lissajous)
The 3D module rotates each point around the Y-axis every frame using the standard 2D rotation matrix applied to the x/z plane:

```
x' = x·cos(θ) + z·sin(θ)
z' = −x·sin(θ) + z·cos(θ)
y' = y
```
followed by a simple perspective-divide projection to place it on a 2D canvas. This is the same core operation (matrix transformation of a coordinate vector) used throughout computer graphics and — not coincidentally — throughout machine learning.

### Lissajous Figures
First studied by Jules Antoine Lissajous in 1857, these curves plot two (or three) oscillators against each other:

```
x(t) = sin(a·t)
y(t) = sin(b·t + δ)
```

The ratio `a:b` determines the shape — `1:1` gives an ellipse, `1:2` a figure-eight, `3:2:5` (the 3D module's default) a complex non-repeating braid.

---

## 🎵 Frequency Reference

| Frequency | Musical Note | Context |
|---|---|---|
| 60 Hz | B1 | Lowest bass guitar string |
| 220 Hz | A3 | Default — warm midrange |
| 440 Hz | A4 | Concert pitch (A440) |
| 880 Hz | A5 | Bright treble |

> f = 440 × 2^((n−69)/12), where n is the MIDI note number — the formula behind every note name shown in the app.

---

## 🚀 Getting Started

No installation. No dependencies. Just open a file.

```bash
git clone https://github.com/lanayaberg/wavelab.git
cd wavelab
open index.html
```

Or visit the **[live demo](https://lanayaberg.github.io/wavelab)** directly.

---

## 🏗️ How It's Built

```
wavelab/
└── index.html   # Everything: HTML + CSS + JavaScript
```

One file. No build tools, no npm, no bundler.

### Tech Stack

| Technology | Usage |
|---|---|
| **Canvas 2D API** | All rendering — oscilloscopes, Lissajous trails, epicycles, 3D projection — at 60fps |
| **Web Audio API** | A small polyphonic voice engine (`VoiceEngine`) built on `OscillatorNode` + `GainNode`, supporting simultaneous notes/tones across every module |
| **CSS Custom Properties** | Live, scoped color theming — each module's accent color updates instantly without touching JS-driven layout |
| **requestAnimationFrame** | A single master loop dispatches to whichever module is active, keeping idle tabs at zero cost |
| **Pointer Events** | Unified mouse/touch/pen handling for the piano keys and the 3D drag-to-rotate interaction |

### Key Implementation Details

**Polyphonic audio engine** — Rather than one hard-coded oscillator, `VoiceEngine` manages a `Map` of independently addressable voices by ID, so the Piano can hold multiple notes at once, the Mixer can play two custom waveforms simultaneously, and the 3D module can play a three-note chord — all through the same small API (`play`, `update`, `stop`).

**Fourier epicycles** — Each harmonic term becomes a rotating vector; the vectors are chained tip-to-tail, and the y-coordinate of the final tip *is* the partial Fourier sum at that instant, drawn live as a scrolling trace alongside the circles that produced it.

**3D projection without a 3D library** — The Lissajous module hand-rolls a Y-axis rotation matrix and a perspective divide rather than pulling in Three.js, keeping the zero-dependency philosophy intact while still producing a convincing sense of depth (particles shrink and dim as they recede).

**Tab-scoped color theming** — Only the Waveform Lab's own DOM subtree listens to its dynamic `--color` custom property; every other module keeps the app's default teal, so switching wave types in one tab never bleeds into another.

---

## 🧠 What I Learned Building This

- **Canvas 2D rendering** — coordinate systems, phosphor-fade trail effects, shadow/glow rendering, and keeping a single `requestAnimationFrame` loop lean across five very different visualizations
- **Web Audio API** — building a reusable polyphonic voice manager, envelope shaping to avoid clicks/pops, and mixing multiple live oscillators
- **Fourier analysis** — implementing the actual series (not just describing it) for square, sawtooth, and triangle waves, and watching Gibbs phenomenon appear naturally at low harmonic counts
- **3D→2D projection** — rotation matrices and perspective-divide, applied by hand
- **Interaction design** — keyboard shortcuts, pointer-based drag-to-rotate, and touch-friendly piano keys, all sharing one input model
- **CSS custom properties as a theming system** — scoping dynamic state to a subtree instead of the global root to avoid cross-component leakage

---

## 📄 License

MIT License — do whatever you want with it.

---

<div align="center">

Built with curiosity, math, and too much coffee.

**[⭐ Star this repo if you found it interesting](https://github.com/lanayaberg/wavelab)**

</div>
