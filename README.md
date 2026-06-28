[README.md](https://github.com/user-attachments/files/29438315/README.md)
# TempoMarkerA

**Beat-accurate timeline markers and keyframe snapping for Blender 5.x**

> Concept & idea by **AleXx**  
> Built with AI assistance (Claude by Anthropic)

---

## ⚠️ Important note

**TempoMarkerA only appears in the Dope Sheet editor.**

To access it: open the **Dope Sheet** → press `N` to open the sidebar → find the **Tempo Align** tab on the right.

It does not appear in the 3D Viewport, NLA Editor, Graph Editor, or any other editor. This is intentional — the Dope Sheet is where you work with keyframes directly, making it the most natural place for beat-alignment tools.

---

## What is this?

TempoMarkerA solves a problem no existing addon handles properly for Blender 5.x: **aligning your animation timeline to a musical tempo**.

Whether you're creating motion graphics synced to music, VJ loops, esports broadcast animations, or any rhythm-driven visual — manually counting frames per beat is tedious and error-prone. TempoMarkerA automates it.

---

## Features at a glance

- 🎵 **Beat Marker Generation** — places timeline markers at every beat or every bar
- 🔗 **Snap Keyframes to Beat** — snaps existing keyframes to the nearest beat
- ⏩ **Beat Navigation** — jump the playhead beat by beat
- 📐 **Live readout** — shows frames-per-beat in real time

---

## Compatibility

| Blender | Status |
|---------|--------|
| 5.x | ✅ Fully supported |
| 4.2 – 4.x | ✅ Should work |
| 3.x and below | ❌ Not supported |

Python 3.13 (bundled with Blender 5.1). No external dependencies.

---

## Installation

1. Download `TempoMarkerA_v1.0.zip` from the [Releases](../../releases) page
2. In Blender: **Edit → Preferences → Add-ons → Install from Disk**
3. Select the zip file
4. Enable the checkbox next to **TempoMarkerA**

**To uninstall:** Edit → Preferences → Add-ons → find TempoMarkerA → click the dropdown arrow → **Remove**

---

## How to use

Open the **Dope Sheet**, press `N`, click the **Tempo Align** tab.

---

### 🎵 Tempo section

This is where you configure your music's timing.

| Field | What it does |
|-------|-------------|
| **BPM** | Beats per minute of your music. Use a BPM tap app on your phone if you're not sure |
| **Beats/Bar** | How many beats per measure — `4` for 4/4 time, `3` for 3/4, etc. |
| **Offset (frames)** | The frame where beat 1 lands. Leave at `0` if your music starts at the beginning. If your music comes in at frame 48 for example, set this to `48` |
| **Mark every beat** | **Off** = one marker per bar (less clutter). **On** = one marker per beat (more precise) |

Below these fields, a grey readout shows:
```
24.000 fps  →  8.727 frames / beat
```
This tells you exactly how many frames fall between each beat at your current BPM and FPS. Useful to double-check before generating markers.

---

### ⏩ Jump to beat

Two arrow buttons `◀ ▶` that move the playhead to the **previous** or **next** beat instantly.

Use this when placing keyframes manually — instead of calculating which frame a beat lands on, just press ▶ to jump there.

---

### 📍 Beat Markers section

**Generate Beat Markers** — reads your BPM, Beats/Bar, and Offset, then places markers across the entire frame range of your scene.

Marker naming format:
- With **Mark every beat OFF**: `Bar1`, `Bar2`, `Bar3`...
- With **Mark every beat ON**: `B1.1`, `B1.2`, `B1.3`, `B1.4`, `B2.1`, `B2.2`... (Bar.Beat)

**Clear Beat Markers** — removes only the markers that TempoMarkerA created. Any markers you placed manually are left untouched.

> Re-running Generate automatically clears previous TempoMarkerA markers first, so you can freely change BPM and regenerate without duplicates.

---

### 🔗 Snap Keyframes section

After roughing in your animation, use this to lock all keyframes onto the beat grid.

**Snap Mode dropdown:**
- `Selected Keyframes` — only snaps keyframes you have highlighted/selected in the Dope Sheet
- `All Keyframes` — snaps every keyframe on every selected object, regardless of selection

**Snap Threshold (frames):**
- `999` (default) — snaps every keyframe to its nearest beat, no matter how far away
- e.g. `6` — only snaps keyframes that are already within 6 frames of a beat; keyframes farther away are left alone

**Snap Keyframes to Beat** button — runs the snap. Works on Object actions, NLA strips, Shape Keys, and Shader node animation data.

> This operation is fully undoable — press `Ctrl+Z` if the result isn't what you wanted.

---

## Typical workflow

```
1. Load your music into the VSE or set your scene frame range
2. Open Dope Sheet → N → Tempo Align tab
3. Enter BPM (e.g. 128) and Beats/Bar (e.g. 4)
4. Set Offset if music doesn't start at frame 0
5. Click Generate Beat Markers → timeline fills with Bar1, Bar2...
6. Animate roughly, using ◀ ▶ to jump to beats as you work
7. When done → Snap Keyframes to Beat to lock everything on the grid
```

---

## Why this exists

There are a few BPM marker addons on GitHub — but they all use the legacy `bl_info` format and break on Blender 4.2+. None of them have keyframe snapping. TempoMarkerA is the first Extension-format addon that combines both features, built specifically for Blender 5.x.

The idea came from a real workflow need: **AleXx** wanted a tool like this and couldn't find one that worked. So it got built.

---

## Roadmap

- [ ] Tap Tempo button (tap along to music to calculate BPM)
- [ ] Beat grid overlay drawn directly on the Dope Sheet
- [ ] Multi-tempo support (change BPM mid-timeline)
- [ ] Auto-detect BPM from a loaded audio strip

PRs and issues welcome.

---

## License

GPL-2.0-or-later — same as Blender itself. Free to use, modify, and share.

---

## Credit

- **Concept & idea**: AleXx
- **Code**: Built with AI assistance (Claude by Anthropic)
- Inspired by the gap left by legacy addons that stopped working on modern Blender versions
