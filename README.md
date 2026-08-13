# FAISS GPU CUDA cuVS wheels

Validated, unofficial FAISS GPU wheels with NVIDIA cuVS support for CUDA 12
and CUDA 13. The CUDA variants are separate PyPI distributions because their
runtime dependency sets are mutually exclusive.

## PyPI projects

- [faiss-gpu-cu12-cuvs](https://pypi.org/project/faiss-gpu-cu12-cuvs/)
- [faiss-gpu-cu13-cuvs](https://pypi.org/project/faiss-gpu-cu13-cuvs/)

The existing CUDA 12 releases, repository wheel, and original build notes
remain preserved in [LEGACY-CU12-1.14.1.post1.md](LEGACY-CU12-1.14.1.post1.md).

## Version 1.15.0

| Property | CUDA 12 variant | CUDA 13 variant |
|---|---|---|
| Package | `faiss-gpu-cu12-cuvs` | `faiss-gpu-cu13-cuvs` |
| Version | `1.15.0` | `1.15.0` |
| Python | CPython 3.12 | CPython 3.12 |
| Platform | Linux x86-64 / WSL2 / Ubuntu 24.04+ | Linux x86-64 / WSL2 / Ubuntu 24.04+ |
| Wheel tag | `manylinux_2_39_x86_64` | `manylinux_2_39_x86_64` |
| CUDA target | 12.9 Update 1 | 13.0 |
| cuVS / RAFT / RMM | 26.6.0 | 26.6.0 |
| Native GPU code | `sm_75`, `sm_80`, `sm_86`, `sm_90` | `sm_75`, `sm_80`, `sm_86`, `sm_90` |
| Validated GPU | RTX 3090 (`sm_86`) | RTX 3090 (`sm_86`) |

Repository copies, also attached to the `v1.15.0` release:

- [`faiss_gpu_cu12_cuvs-1.15.0-cp312-cp312-manylinux_2_39_x86_64.whl`](wheels/faiss_gpu_cu12_cuvs-1.15.0-cp312-cp312-manylinux_2_39_x86_64.whl)
- [`faiss_gpu_cu13_cuvs-1.15.0-cp312-cp312-manylinux_2_39_x86_64.whl`](wheels/faiss_gpu_cu13_cuvs-1.15.0-cp312-cp312-manylinux_2_39_x86_64.whl)

See [SHA256SUMS-1.15.0.txt](SHA256SUMS-1.15.0.txt) for release hashes and
[VALIDATION.md](VALIDATION.md) for the executed test coverage. The permanent
release notes are in [RELEASE_NOTES-1.15.0.md](RELEASE_NOTES-1.15.0.md).

## Installation

Choose exactly one FAISS CUDA variant in an environment.

CUDA 12.9 / PyTorch cu129:

```bash
pip install --extra-index-url https://pypi.nvidia.com \
  faiss-gpu-cu12-cuvs==1.15.0
```

CUDA 13.0 / PyTorch cu130:

```bash
pip install --extra-index-url https://pypi.nvidia.com \
  faiss-gpu-cu13-cuvs==1.15.0
```

The wheels pin their CUDA and RAPIDS runtime packages. The host still requires
a compatible NVIDIA driver. FAISS does not link cuDNN directly; coexistence was
validated with the cuDNN packages selected by the corresponding PyTorch 2.9.1
wheel.

## Validated stacks

CUDA 12:

```text
torch==2.9.1+cu129
torchaudio==2.9.1+cu129
torchvision==0.24.1+cu129
flash-attn==2.8.3 (cu12 / torch 2.9 / CXX11 ABI true asset)
triton==3.5.1
```

CUDA 13:

```text
torch==2.9.1+cu130
torchaudio==2.9.1+cu130
torchvision==0.24.1+cu130
flash-attn==2.8.3 (cu13 / torch 2.9 / CXX11 ABI true asset)
triton==3.5.1
xformers==0.0.33.post2
```

CUDA 13.3 is not claimed because its runtime failed device discovery on the
validated WSL2 system. CUDA 12.9.0 is not claimed for the exact cu129 stack
because its toolkit metapackage conflicts with PyTorch's cuBLAS 12.9.1.4 pin.

## Legacy CUDA 12 artifact

The prior wheel remains available and is not replaced or removed:

- [faiss_gpu_cu12_cuvs-1.14.1.post1-cp312-cp312-manylinux_2_38_x86_64.whl](wheels/faiss_gpu_cu12_cuvs-1.14.1.post1-cp312-cp312-manylinux_2_38_x86_64.whl)
- [PyPI 1.14.1.post1 release](https://pypi.org/project/faiss-gpu-cu12-cuvs/1.14.1.post1/)

## Provenance

- FAISS: upstream `v1.15.0`
- Packaging scaffold: [Di-Is/faiss-gpu-wheels](https://github.com/Di-Is/faiss-gpu-wheels)
- cuVS integration guidance: [GPU Faiss with cuVS](https://github.com/facebookresearch/faiss/wiki/GPU-Faiss-with-cuVS)

These are downstream wheel builds, not official Meta or NVIDIA artifacts.
Third-party components remain governed by their respective licenses.

## License

See [LICENSE](LICENSE). Third-party FAISS, cuVS, RAPIDS, CUDA, and packaging
components retain their own license terms.
