# Santosh

Computer vision enthusiast building real-time detection and tracking for industrial environments.

I point cameras at moving objects on the floor — boxes, pallets, people, product — and turn that into a count and a record. The point is reliable evidence, so a team is not standing on a line clicking a counter or scrubbing footage after the fact.

Most of this was built part-time and mostly solo: no computer-vision team, no dedicated infrastructure, a GPU and a camera, fitted in around the rest of the work.

---

## What I build

| Capability | What it is for |
|------------|----------------|
| Detection & tracking | Live pipelines that lock onto an object across frames and count it once |
| Operational evidence | A timestamped record that can be checked against the count people already trusted |
| Multi-camera inference | More streams per GPU by matching frame rate to the process, not to video playback |

---

## A line that had to be counted

People were standing at a conveyor, clicking a counter every time a box went by. It worked. It did not scale, it left almost no audit trail, and it spent hours that did not need to be spent that way.

The pipeline that replaced it is straightforward: a top-down camera, YOLOv8 for detection, ByteTrack so each box is followed across frames and counted once. It runs live on a production line and was checked against the existing manual-count baseline. That was the proof that cameras counting product was a system you could run, not a demo.

The counts did not match at first. The usual response is more labels and another training run. The model was already right. At the pick point, operator hands were covering the lens as the box passed, so the camera never saw the object. A mount change fixed what more training images would not.

Scaling raised a different limit. The GPU, not the CPU, caps how many streams you can run. This process does not need 25–30 frames per second. It needs enough frames to not miss a box. Dropping the frame rate to what the line actually requires is what lets one GPU carry more cameras. The target is the same system on sixteen lines, not a GPU per camera.

Along the way, threshold tuning started reading stale files. The codebase was sitting in a cloud-synced folder. Moving active work to a plain local path ended that. Saved frames and a live stream are also different failure modes: model accuracy gets checked on saved frames before a live camera is blamed.

---

## The same habits on a second problem

Once counting was real, the same capture rules were pointed at reading pallet labels at a dock door: do not trust the stream blindly, and prove the idea on a phone and a laptop before buying hardware.

---

## What held up

- A live count on a real line, checked against the manual baseline
- An accuracy gap traced to mounting and occlusion, not to a model that needed retraining
- A scaling path based on process frame rate, meant to survive a facility layout change rather than a one-line demo
- The same validation habits carried into a second, separate vision problem
- All of it part-time and mostly solo, without a formal computer-science background

---

## How I work

- Check whether the camera can see the object before you retrain
- Lighting and mount beat a more expensive camera with a bad view
- Prove it cheaply before you buy hardware
- Keep active code on local disk, not in a cloud-synced folder
- Separate saved-frame tests from live-stream failures

---

## Stack

Python · YOLOv8 · OpenCV · ByteTrack · PyTorch · TensorFlow · Label Studio · Roboflow · industrial IP cameras

---

## Currently

- Taking a single working line to many lines and more than one site
- False positives when something occludes the object, including glare and wrap
- GPU use across concurrent feeds, and tracking when frames drop
- Inference at the edge (Jetson, IPUs)
- An audit record for the line, rather than a verbal confirmation

Next, where the same cameras already look: anomalies in how work moves, throughput forecasting from the count, and people counting in receiving and shipping.

---

Most of the production work stays private — client deployments, models, and site-specific pipelines. Happy to walk through the architecture and the results.
