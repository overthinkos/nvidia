# image/nvidia — signpost (not the rule-set)

This submodule is the **NVIDIA / GPU runtime** image family (base for all
GPU-accelerated images): a `charly.yml` (plus per-kind sibling files) that imports the main repo
under the `charly` namespace and `build.yml` flat.

**Load these skills FIRST (R0):**

- `/charly-distros:nvidia` — the NVIDIA GPU base image (Fedora).
- `/charly-distros:nvidia-layer` — the GPU runtime layer.
- `/charly-distros:cuda` — CUDA toolkit / cuDNN / ONNX runtime.
- `/charly-distros:rocm` — the AMD ROCm runtime.

**Authoritative rules live in the `opencharly` superproject's root `CLAUDE.md`**
(R0–R10, hard-cutover, AI attribution, git-workflow). This file only signposts
and restates no rule. The multi-agent workflow is in `/charly-internals:agents`.
History lives in `CHANGELOG.md`.
