# FAISS GPU cuVS 1.15.0

This release adds separately installable CUDA 12 and CUDA 13 distributions.
Choose one variant per Python environment.

## Wheels

- `faiss-gpu-cu12-cuvs==1.15.0`: CUDA 12.9 Update 1
- `faiss-gpu-cu13-cuvs==1.15.0`: CUDA 13.0

Both wheels target CPython 3.12 on Linux x86-64 and contain native CUDA code
for `sm_75`, `sm_80`, `sm_86`, and `sm_90`. They were executed on an RTX
3090 (`sm_86`) under Ubuntu 24.04 on WSL2.

## Integrity

```text
20e104ce0754ce53fd5d4bee1036ab8aae2f354f8248fa055adbeeb7a38fc63f  faiss_gpu_cu12_cuvs-1.15.0-cp312-cp312-manylinux_2_39_x86_64.whl
2954f14bef772a206841898c429911a6b28dba589a1912f541785396e7e9cb28  faiss_gpu_cu13_cuvs-1.15.0-cp312-cp312-manylinux_2_39_x86_64.whl
```

See `VALIDATION.md` for the executed GPU and packaging checks. Earlier CUDA
12 releases and the checked-in 1.14.1.post1 wheel remain available unchanged.
