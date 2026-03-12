# Unity 2022.3.62f3 - Reverse Engineering PDBs

release notes: https://unity.com/releases/editor/whats-new/2022.3.62f3

---

## Unity Player PDBs

found at:
```
\Unity\Hub\Editor\2022.3.62f3\Editor\Data\PlaybackEngines\windowsstandalonesupport\Variations\win64_player_nondevelopment_mono
```

files in this folder:
```
nvngx_dlss.dll
NVUnityPlugin.dll
UnityCrashHandler64.exe
UnityCrashHandler64.pdb
UnityPlayer.dll
UnityPlayer_Win64_player_mono_x64.pdb  <-- link this in IDA or Ghidra
WindowsPlayer.exe
WindowsPlayer_player_Master_mono_x64.pdb
```

---

## PhysX 4.1 - Building Debug PDBs

unity 2022.3 uses physx 4.1, building debug gives you full struct layouts for all physx::, Sc::, Np:: types

```cmd
git clone https://github.com/NVIDIAGameWorks/PhysX
cd PhysX
git checkout 4.1
cd physx
mkdir build
cd build

cmake ../compiler/public -G "Visual Studio 18 2026" -A x64 ^
  -DPHYSX_ROOT_DIR="C:\path\to\PhysX\physx" ^
  -DTARGET_BUILD_PLATFORM=windows ^
  -DPX_BUILDSNIPPETS=OFF ^
  -DPX_BUILDPUBLICSAMPLES=OFF ^
  -DCMAKE_BUILD_TYPE=Debug ^
  -DPX_OUTPUT_LIB_DIR="C:\path\to\PhysX\physx\build\lib" ^
  -DPX_OUTPUT_BIN_DIR="C:\path\to\PhysX\physx\build\bin"

cmake --build . --config Debug
```

change the generator to match your VS version, run `cmake --help | findstr "Visual Studio"` to find it

pdbs will be in:
```
C:\path\to\PhysX\physx\build\bin\debug\
```
