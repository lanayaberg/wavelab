# 〰️ WaveLab — Mathematical Wave Synthesizer

> An interactive mathematical wave synthesizer that lets you **see** and **hear** the physics of sound — built with pure HTML, CSS, and JavaScript.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![Web Audio API](https://img.shields.io/badge/Web_Audio_API-4cc9f0?style=flat)
![Canvas 2D](https://img.shields.io/badge/Canvas_2D-b14aed?style=flat)
![No dependencies](https://img.shields.io/badge/dependencies-none-00f5d4?style=flat)

**[🚀 Live Demo →](https://lanayaberg.github.io/wavelab)**

---

## ✨ What is this?

WaveLab is an interactive tool that visualizes **mathematical wave functions** in real time — complete with sound synthesis. Adjust frequency, amplitude, phase, and harmonics while watching the math unfold on screen and hearing it through your speakers.

It's both a **creative toy** and a **learning tool** for understanding the physics and mathematics behind sound.

---

## 🎛️ Features

| Feature | Description |
|---|---|
| **Oscilloscope** | Real-time animated wave with CRT phosphor glow effect |
| **Lissajous Figure** | XY plot showing two frequencies combined — reveals hidden geometric patterns |
| **Harmonic Spectrum** | Visual spectrum analyzer showing the amplitude of each harmonic |
| **Sound Synthesis** | Real audio output via Web Audio API — hear what you see |
| **5 Wave Types** | Sine, Square, Sawtooth, Triangle, Fourier series |
| **4 Live Controls** | Frequency (60–880 Hz), Amplitude, Phase shift, Harmonics |
| **Live Formula** | Mathematical formula updates in real time as you adjust parameters |
| **Music Theory** | Shows the musical note, period, wavelength, and angular frequency |
| **Zero Dependencies** | Pure HTML/CSS/JS — no frameworks, no libraries, no build step |

---

## 🌊 The Wave Types

### Sine Wave
The fundamental building block of all sound. Pure, smooth, mathematically perfect.

```
y(t) = A · sin(2π · f · t + φ)
```

### Square Wave
Jumps instantly between +1 and −1. Rich in odd harmonics — sounds like a retro video game.

```
y(t) = A · sgn(sin(2π · f · t + φ))
```

Fourier decomposition: `y = (4/π)[sin(x) + sin(3x)/3 + sin(5x)/5 + ...]`

### Sawtooth Wave
Rises linearly then drops sharply. Contains **all** harmonics — the brightest, most aggressive tone.

```
y(t) = A · 2(f·t − ⌊f·t + 0.5⌋)
```

### Triangle Wave
Rises and falls linearly. Only odd harmonics like square, but they fall off much faster — a softer sound.

```
y(t) = A · (2/π) · arcsin(sin(2π · f · t))
```

### Fourier Series
The key insight of mathematics: **any** periodic wave can be built from sine waves. Watch as adding more harmonics progressively approximates a square wave.

```
y(t) = (4/π) · Σ sin((2k−1)·2π·f·t) / (2k−1),  k = 1, 2, 3, ...
```

---

## 📐 The Math Behind It

### Lissajous Figures
The Lissajous canvas plots two oscillators against each other on X and Y axes:

```
x(t) = A · sin(ω₁ · t)
y(t) = B · sin(ω₂ · t + φ)
```

The ratio ω₁/ω₂ determines the shape:
- `1:1` → Ellipse or circle (depending on phase)
- `1:2` → Figure eight
- `1:3` → Three-looped curve
- `2:3` → Pretzel shape

These patterns were first studied by **Jules Antoine Lissajous** in 1857 and are still used today to measure frequency ratios on oscilloscopes.

### Why Phase Matters
The phase shift `φ` slides the wave horizontally without changing its shape or frequency. When two waves are **in phase** (φ=0) they add constructively — when **out of phase** (φ=π) they cancel completely. This is the physics of noise-cancelling headphones.

### Fourier's Big Idea
Joseph Fourier proved in 1822 that any periodic function — no matter how complex — can be expressed as an infinite sum of sine waves. This theorem is the foundation of:
- Digital audio (MP3, AAC)
- Image compression (JPEG)
- Signal processing
- Quantum mechanics

You can see it in action: move the **Harmonics** slider while in Fourier mode and watch a perfect square wave gradually emerge from overlapping sines.

---

## 🎵 Frequency Reference

| Frequency | Musical Note | Context |
|---|---|---|
| 60 Hz | B1 | Lowest bass guitar string |
| 110 Hz | A2 | Standard bass |
| 220 Hz | A3 | Default — warm midrange |
| 440 Hz | A4 | Concert pitch (A440) |
| 880 Hz | A5 | Bright treble |

> The relationship between musical notes follows the formula: **f = 440 × 2^((n−69)/12)** where n is the MIDI note number.

---

## 🚀 Getting Started

No installation. No dependencies. Just open a file.

```bash
# Clone the repo
git clone https://github.com/lanayaberg/wavelab.git

# Open in your browser
open index.html
# or just double-click the file
```

Or visit the **[live demo](https://lanayaberg.github.io/wavelab)** directly.

---

## 🏗️ How It's Built

Everything lives in a single `index.html` file. No build tools, no npm, no frameworks.

```
wavelab/
└── index.html   # Everything: HTML + CSS + JavaScript
```

### Tech Stack

| Technology | Usage |
|---|---|
| **Canvas 2D API** | Oscilloscope and Lissajous rendering at 60fps |
| **Web Audio API** | Real-time sound synthesis with OscillatorNode |
| **CSS Custom Properties** | Live color theming — each wave type has its own color palette |
| **requestAnimationFrame** | Smooth 60fps animation loop |
| **Google Fonts** | Space Grotesk + JetBrains Mono |

### Key Implementation Details

**Oscilloscope rendering** — The wave is sampled at every pixel column. A "ghost" copy is drawn at half-speed and lower opacity to create the phosphor afterglow (CRT effect). CSS scanlines add the finishing touch.

**Lissajous trail** — Each frame adds a new point to a trail array. Older points are drawn with lower opacity — the phosphor fade effect. The trail length is inversely proportional to frequency to keep the figure readable at all speeds.

**Sound synthesis** — Web Audio API's `OscillatorNode` directly supports all four standard waveforms. For Fourier mode, sawtooth is used as the closest approximation.

**Color theming** — A single CSS custom property `--color` drives the entire visual theme — wave stroke, glow, slider thumb, badge colors, Lissajous trail, and spectrum bars all update instantly when you switch wave types.

---

## 📸 Screenshots

| Sine Wave | Fourier Series | Square Wave |
|---|---|---|
| Smooth, pure | Built from harmonics | Sharp edges, rich tone |

---

## 🧠 What I Learned Building This

- **Canvas 2D rendering** — coordinate systems, transforms, shadow/glow effects, frame-by-frame animation
- **Web Audio API** — `AudioContext`, `OscillatorNode`, `GainNode`, envelope shaping (linear ramp to avoid clicks)
- **Fourier analysis** — why any wave can be decomposed into sines, and how convergence works visually
- **Lissajous figures** — parametric equations and the geometric relationship between frequency ratios
- **CSS custom properties** — using them as a live theming system driven by JavaScript
- **Performance** — keeping `requestAnimationFrame` loops lean, batching DOM reads, avoiding layout thrash

---

## 🔭 Roadmap / Ideas

- [ ] Oscilloscope zoom and pan
- [ ] Two-wave mixer (add waves together)
- [ ] Record and export audio (.wav)
- [ ] Piano keyboard to play notes
- [ ] 3D Lissajous figure (three oscillators)
- [ ] Frequency modulation (FM synthesis)

---

## 📄 License

MIT License — do whatever you want with it.

---

<div align="center">

Built with curiosity, math, and too much coffee.

**[⭐ Star this repo if you found it interesting](https://github.com/lanayaberg/wavelab)**

</div>
