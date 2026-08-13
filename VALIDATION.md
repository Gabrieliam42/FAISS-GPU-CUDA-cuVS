# FAISS GPU cuVS 1.15.0 validation

Both wheels were installed in separate Python 3.12 environments and executed
on an RTX 3090 (`sm_86`) under WSL2 with Ubuntu 24.04.

## Results per wheel

- Dependency consistency: passed (`uv pip check`)
- Integrated exact-stack GPU harness: passed
- Wheel smoke and Torch CUDA interop: 48 passed, 1 skipped
- Complete upstream FAISS GPU suite: 100 passed, 11 skipped
- Native CUDA images: 192 each for `sm_75`, `sm_80`, `sm_86`, and `sm_90`
- ZIP CRC, wheel RECORD hashes, metadata, tags, and `twine check`: passed

The integrated harness covered import before Torch, classic FAISS GPU flat
search, cuVS flat search, cuVS KNN, cuVS IVFFlat, CAGRA, direct Torch CUDA
tensor interop, FlashAttention, torchvision CUDA NMS, torchaudio CUDA
resampling, and Triton through `torch.compile`. The CUDA 13 environment also
covered xformers memory-efficient attention.

## Upstream numerical test

The complete Python suite produced 1 failed, 1,285 passed, 210 skipped, and
714 passing subtests. The sole failure is the unchanged CPU-only
`test_update_codebooks_with_double` LSQ numerical assertion. It reproduces
with FAISS 1.14.1 and is not a CUDA, cuVS, GPU, or packaging regression. No
FAISS algorithm or upstream test was changed.
