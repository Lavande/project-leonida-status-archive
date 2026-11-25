# Project Leonida Local Build Environment Checklist

> Complete illustrated tutorial & Windows 11 troubleshooting: [gtaleonida.net/leonida-build-tutorial](https://gtaleonida.net/leonida-build-tutorial)
> Interactive PC readiness checker: [gtaleonida.net/can-i-run-leonida](https://gtaleonida.net/can-i-run-leonida)

## Prerequisites

- **OS**: Windows 10/11 64-bit (native runtime) or Linux 64-bit (portable tools + Proton runtime)
- **Free Disk Space**: ~350 GB free SSD space (NVMe strongly recommended for asset extraction and 26,503 shader translations)
- **Python**: 3.12 or newer (`python --version`)
- **.NET SDK**: .NET 8 SDK (`dotnet --list-sdks`)
- **Vulkan SDK**: LunarG Vulkan SDK with `spirv-val` on `PATH`
- **LLVM**: LLVM built with the `AMDGPU` target (`llvm-objdump --version` / `llc --version`)
- **C++ Build Tools (Windows)**: Visual Studio 2022 with the *Desktop development with C++* workload and CMake

## Quick Verification Commands (PowerShell / Bash)

```bash
git --version
python --version
dotnet --list-sdks
cmake --version
spirv-val --version
```

## Common Pitfalls

1. **Missing submodules**: Always clone with `git clone --recursive` or run `git submodule update --init` so `tools/rpf9dump` is populated.
2. **Insufficient free space**: Ensure at least 350 GB is free on the target volume before running `make_game.py`.
3. **Missing `spirv-val` or LLVM on `PATH`**: Restart your terminal after installing the Vulkan SDK and LLVM so environment variables take effect.
4. **Running unit tests with `-I`**: Standard-library tests run with `python -I tests/test_<name>.py`, while pytest-based tests require `python -m pytest tests/test_<name>.py`.
