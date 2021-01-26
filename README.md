# AMD-TrueAudioNext-Complete
AMD's TrueAudio NEXT, ready to compile in one self-contained repository.

## Platform support
- Windows: ✅
- macOS: ✅ (Intel)
- Linux: ✅
  - Note: You must have OpenCL installed, on Fedora use `ocl-icd-devel`

## How to build
1. Clone repository and cd into root directory
2. Execute relevant `init-*` script for your platform
3. Open the `build` directory and open relevant IDE project or execute relevant compilation command
   - For any build system: `cmake --build . --target TrueAudioNext` 
