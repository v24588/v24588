# 👋 Santosh | Real-Time Detection & Tracking

**Teaching cameras to count things so humans don't have to squint at warehouse footage all day.**

[![Python](https://img.shields.io/badge/Python-3.9+-3776ab?logo=python&logoColor=white)](https://www.python.org/)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Powered-FF6D00)](https://github.com/ultralytics/ultralytics)
[![Status](https://img.shields.io/badge/Status-Scaling%20Up-green)](https://github.com/v24588)

---

## What I Build

Point cameras at moving objects → computer says "that's the thing" → count goes up 🔢⬆️

| Capability | Impact |
|-----------|--------|
| **Object Detection** | Boxes, pallets, people, products, whatever moves |
| **Audit Trail** | Turn "cross my heart" into documented proof |
| **Multi-Feed Scaling** | Squeeze more cameras per GPU without losing your mind |

---

## 📖 The Origin Story

It started with a spreadsheet problem wearing a computer vision costume.

Somewhere in a production facility, humans were standing at conveyor lines, manually clicking a counter every time a box went by. It worked. It also didn't scale, didn't leave much of an audit trail, and quietly burned a lot of hours that could go somewhere more useful.

The pitch was simple: point a camera at the line, let software do the counting, keep humans doing things humans are actually good at. The catch was that "simple" and "simple to build" are not the same sentence, and this was a part-time, mostly-solo build, squeezed in alongside everything else on the plate.

No CV team. No dedicated infra. Just a GPU, a camera, a growing respect for how much can go wrong between "the box moved" and "the count is right."

---

## 🗺️ The Journey So Far

<details>
<summary><b>Chapter 1 — First Camera, First Model</b></summary>
<br>

Stood up the first pipeline: top-down camera → YOLOv8 detection → ByteTrack to follow each box across frames so it only gets counted once. Got it running live on one conveyor line. Watching a bounding box lock onto a moving box for the first time felt like the whole project had a pulse.

**Outcome:** proof that "cameras counting boxes" wasn't a science project. It was a real, shippable idea.
</details>

<details>
<summary><b>Chapter 2 — The Great Accuracy Chase</b></summary>
<br>

Then came the fun part: the numbers didn't match the manual counts. Classic instinct says "fix the model." So: more training data, more label corrections, more tuning.

Eventually the real culprit showed up: at the pick point, operator hands were physically blocking the lens right as boxes passed. The model was never wrong. The camera just couldn't see what it wasn't allowed to see.

**Lesson learned the hard way:** before you retrain a model, check whether physics is the problem, not math. A mount change fixes what a thousand more training images never will.
</details>

<details>
<summary><b>Chapter 3 — The OneDrive Betrayal</b></summary>
<br>

Somewhere in the middle of threshold tuning, files started quietly lying: edits wouldn't reflect, reads returned stale data, and debugging turned into "wait, is this even the code I just saved?" Root cause: OneDrive sync fighting the local dev workflow behind the scenes.

**Fix:** moved the entire codebase to a plain local path. Lesson tattooed on the brain: active development and cloud-synced folders do not mix.
</details>

<details>
<summary><b>Chapter 4 — Scaling Math</b></summary>
<br>

One line working well raised the obvious next question: what about all sixteen? Turns out the GPU, not the CPU, is what actually limits how many camera streams you can run at once. The unlock: warehouse counting doesn't need 25–30 fps; it needs enough frames to not miss a box. Dropping frame rate multiplied how many cameras a single GPU could carry, for free.

**Outcome:** a real scaling path instead of "buy a GPU per camera and pray."
</details>

<details>
<summary><b>Chapter 5 — Beyond Boxes</b></summary>
<br>

With counting proven out, the same instincts (reliable capture, don't trust the stream blindly, validate against saved frames before going live) got pointed at a new problem: reading pallet labels at dock doors with nothing but a phone camera and some decode software, before spending a dollar on hardware.

**Philosophy carried forward:** prove it cheap before you build it expensive.
</details>

---

## 🛠️ Tech Stack

<div align="center">

![Python](https://img.shields.io/badge/Python-3776ab?style=for-the-badge&logo=python&logoColor=white)
![YOLOv8](https://img.shields.io/badge/YOLOv8-FF6D00?style=for-the-badge&logo=opencv&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![ByteTrack](https://img.shields.io/badge/ByteTrack-412991?style=for-the-badge)
![Label Studio](https://img.shields.io/badge/Label%20Studio-1E90FF?style=for-the-badge)
![Roboflow](https://img.shields.io/badge/Roboflow-00A8E8?style=for-the-badge)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)

</div>

---

## 📌 Pinned Projects

**Most of my best work is private**

| Project | Stack | Status |
|---------|-------|--------|
| **warehouse-vision** | YOLOv8 · ByteTrack · OpenCV | Active, live on production line(s), scaling to more |
| **dock-scanning** | Barcode/label decode pipelines | Phase 0 validation |

> Want to see the good stuff? [Ask me about it.](https://github.com/v24588)

---

## 📊 Contribution Highlights

<div align="center">

![Total Contributions](https://img.shields.io/badge/Total%20Repos-5+-blue?style=flat-square)
![Primary Language](https://img.shields.io/badge/Primary%20Language-Python-3776ab?style=flat-square)
![Focus Area](https://img.shields.io/badge/Focus-Computer%20Vision%20%26%20Detection-FF6D00?style=flat-square)

</div>

**Current Activity:**
- 🎯 Scaling from single-line to multi-warehouse deployment
- 🔬 Optimizing GPU utilization for multi-feed inference
- 📈 Building industry-grade audit systems

---

## 💡 Major Outcomes So Far

- ✅ Live deployment counting real product on a real production line, validated against the existing manual-count baseline
- ✅ Root-caused an accuracy gap to a hardware/mounting issue instead of burning weeks retraining a model that was never broken
- ✅ Built a scaling architecture designed to survive a facility layout change before it even happens
- ✅ Carried the same reliability patterns (stream handling, validation discipline) into a second, unrelated CV problem
- ✅ Did all of it part-time, mostly solo, without a formal CS background, just stubbornness and a decent GPU

---

## The Hard-Won Lessons

- 🗂️ **Local files only.** OneDrive + active codebase = files that lie to you.
- 🎥 **Lighting > Gear.** A cheap camera with great lighting beats expensive gear with bad lighting, every time.
- 🐌 **Lower your FPS.** 25 fps is overkill for warehouse counting. Drop it, fit more cameras per GPU.
- 🖐️ **Physics > Models.** Sometimes the model isn't wrong: a human's hand is just in the way.
- 💸 **Prove it cheap first.** Validate the concept on a phone and a laptop before buying a single piece of hardware.
- 🔁 **Isolate your variables.** Test model accuracy on saved frames before blaming a live camera stream; they're different failure modes wearing the same "it's wrong" costume.

---

## 💡 What I'm Working On

```python
# Current challenges:
- Multi-camera synchronization across distributed warehouse sites
- Reducing false positives in occlusion scenarios  
- Optimizing model inference at edge (Jetson, IPUs)
- Real-time tracking consistency across frame drops

# Next frontier:
- Anomaly detection in warehouse workflows
- Predictive analytics for throughput forecasting
- People counting in receiving/shipping zones
```

---

## 📈 Repository Languages

```
Python       ████████████░░  65%
Java         ██░░░░░░░░░░░░  10%
HTML         ░░░░░░░░░░░░░░  15%
Other        ░░░░░░░░░░░░░░  10%
```

---

## 🎯 Focus Areas

**Computer Vision** · **Real-Time Detection** · **Object Tracking** · **Industrial Automation** · **GPU Optimization** · **Multi-Camera Systems**

---

## 🚀 Quick Start

Interested in computer vision, object detection, or industrial automation? Here's where to start:

1. Learn YOLOv8: [Ultralytics Docs](https://docs.ultralytics.com/)
2. Multi-object tracking: [ByteTrack](https://github.com/ifzhang/ByteTrack)
3. Data labeling: [Label Studio](https://labelstud.io/)
4. Dataset prep: [Roboflow](https://roboflow.com/)

---

## Current Mission

Scaling from "it works on one line" to "it works on sixteen": a completely different and much more annoying problem.

The good news? It's solvable. The bad news? There's a GPU somewhere having an existential crisis about it.

---

## The Private Stuff

**47 private contributions** across client projects. Most of my best work is private for good reason:
- Client work & industrial deployments
- Proprietary detection models
- Custom tracking pipelines
- Warehouse-specific optimizations

**It's cooler than this README makes it sound.** [Ask me about it.](https://github.com/v24588)

---

<div align="center">

**Building systems that see what humans can't. One warehouse at a time.** 🎯

*Started with a spreadsheet problem. Ended up teaching cameras to count.*

</div>
