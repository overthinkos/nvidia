# overthinkos/nvidia

The **NVIDIA GPU base image family** for [OpenCharly](https://github.com/overthinkos/overthink),
split into its own repository and mounted as a git submodule at `image/nvidia`
of the main repo.

## What's here

| Kind | Entries |
|---|---|
| `image:` | `nvidia` (GPU base: driver libs + CDI + CUDA toolkit), `python-ml` (GPU ML Python env — PyTorch/transformers/vLLM/llama.cpp, disabled) |

The GPU runtime **layers** (`nvidia`, `cuda`, `python-ml`, `llama-cpp`) are
**not** here — they stay in the main repo. They are shared infrastructure
consumed across many image families (`versa`, `immich-ml`, `jupyter-ml`,
`comfyui`, `unsloth-studio`, `whisper`, `marimo`) and by the
`arch`/`cachyos`/`fedora`/`bootc` base submodules, so by the shared-layer rule
they remain in `github.com/overthinkos/overthink/candy/` and are reached here
by `@github` reference.

## Composition by reference — nothing is vendored

- every layer is an `@github.com/overthinkos/overthink/candy/<name>:<tag>` ref;
- the shared build-config (`build.yml` — distro/builder/init, including the
  `fedora` distro definition + the `rpm` format template) arrives via a flat
  `import:`;
- the Fedora base (`fedora-nonfree`) + the builder (`fedora-builder`) arrive via
  the namespaced `charly` import of the main repo (`charly.fedora-nonfree`,
  `charly.fedora-builder`).

Layer refs + `build.yml` pin to the ecosystem shared-layer tag
(`v2026.141.1600`, the same tag arch/cachyos/fedora pin); the `charly` namespace
pins to the schema tag (`v2026.143.844`). The `nvidia`/`cuda` layers are
unchanged at that tag, so the `nvidia` image is byte-identical to main's
pre-split build.

## Mutual import with main

Main consumes the `nvidia` image as `base: nvidia.nvidia` (its GPU pod families
— `comfyui`, `jupyter-ml`, `jupyter-ml-notebook`, `ollama`,
`unsloth-studio`), and this repo consumes main as
`charly.fedora-nonfree` + `charly.fedora-builder`. The import cycle is broken at load.

## Build

```bash
charly --repo overthinkos/nvidia image build nvidia      # anywhere
charly -C image/nvidia image build nvidia                # from the parent checkout
charly -C image/nvidia image build python-ml --include-disabled
```

## Verification

After `charly box build`:

- `charly eval box nvidia` — build-scope probes (binaries, packages, CDI files).
- GPU runtime probes (`nvidia-smi`, CUDA device presence) require GPU hardware
  and are exercised on a GPU host.

---

*Assisted-by: Claude (analysed on a live system)*
