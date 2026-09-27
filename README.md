# Santosh

Computer vision engineer building real-time detection and tracking for industrial environments — conveyor counting, dock-door label reading, and multi-camera inference on shared GPUs.

[GitHub](https://github.com/v24588)

---

## Focus

| Area | What I ship |
|------|-------------|
| Object detection & tracking | YOLOv8 + ByteTrack pipelines for boxes, pallets, and people on live lines |
| Audit & evidence | Timestamped counts and pallet-integrity photos tied to operational records |
| Multi-feed scaling | More camera streams per GPU by matching frame rate to the process, not to video playback |

---

## Selected work

### Warehouse vision (private)

Live product counting on production conveyor lines. Top-down camera → detection → multi-object tracking so each item is counted once, validated against the existing manual-count baseline.

Notable outcomes:
- Root-caused an accuracy gap to operator hands occluding the lens at the pick point — fixed with mounting/geometry instead of retraining a model that was already correct
- Scaled capacity by lowering FPS to what the process needs, so one GPU carries more feeds
- Moved active development off OneDrive-synced paths after stale reads corrupted the debug loop

**Stack:** Python, YOLOv8, ByteTrack, OpenCV, Label Studio, Roboflow, PyTorch

### DockVision (private) — Phase 0

Dock-door QR / Pallet ID reading while a forklift is stopped at the door, with a path to PO match and tower-light signaling. Hardware-first spend is gated on decode proof.

Current status:
- Decode harness (`zxing-cpp` + QReader) scores a tagged frame corpus from Reolink / NVR captures
- Phase 0 blocked on a **resolution wall** (~1 px/module vs ~3–5 needed); next step is a tighter PTZ zoom re-shoot before further hardware
- Design docs, agent governance, and a weekly research log keep decisions append-only

**Stack:** Python, QReader / YOLOv8 detector, pyzbar, Reolink RTSP + NVR, planned Supabase + WebRelay signaling

---

## Principles I reuse

- Validate on saved frames before blaming a live stream
- Prefer cheap proof (phone / existing PTZ / screenshot corpus) before buying hardware
- Treat lighting, mount, and occlusion as first-class failure modes — not model bugs by default
- Keep active code on local disk, not cloud-synced folders

---

## Tech

Python · YOLOv8 · OpenCV · ByteTrack · PyTorch · TensorFlow · Label Studio · Roboflow · industrial IP cameras / NVR

---

## Currently working on

- Scaling warehouse counting from single-line to multi-line / multi-site
- Clearing DockVision Phase 0 decode (capture resolution before decoder tuning)
- GPU sharing and inference efficiency across concurrent CV workloads

---

*Most client and production code stays private. Happy to walk through architecture and results on request.*
