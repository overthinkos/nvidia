# image/nvidia — signpost (not the rule-set)

This submodule is the **NVIDIA / GPU runtime** image family (base for all
GPU-accelerated images): an `overthink.yml` (plus per-kind sibling files) that imports the main repo
under the `ov` namespace and `build.yml` flat.

**Load these skills FIRST (R0):**

- `/ov-distros:nvidia` — the NVIDIA GPU base image (Fedora).
- `/ov-distros:nvidia-layer` — the GPU runtime layer.
- `/ov-distros:cuda` — CUDA toolkit / cuDNN / ONNX runtime.
- `/ov-distros:rocm` — the AMD ROCm runtime.

**Authoritative rules live in the `overthink` superproject's root `CLAUDE.md`**
(R0–R10, hard-cutover, AI attribution, git-workflow). This file only signposts
and restates no rule. The multi-agent workflow is in `/ov-internals:agents`.
History lives in `CHANGELOG.md`.
