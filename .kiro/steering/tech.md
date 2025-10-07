# Technology Stack

## Build System
- **CMake 3.21.0+** - Primary build system
- **C++17** - Language standard
- Multi-configuration support: Debug, RelWithDebInfo, Release
- Multi-core compilation enabled (MSVC /MP flag)

## Supported Platforms
- Windows (MSVC)
- Linux (GCC) 
- macOS (Clang)
- ARM32/ARM64 and x86/x64 architectures

## Key Technologies
- **TorqueScript** - Built-in scripting language (.tscript extension)
- **OpenGL/DirectX** - Cross-platform rendering
- **SQLite** - Embedded database
- **Platform abstraction layers** - Win32, POSIX, SDL, X11

## Common Build Commands

### Initial Project Setup
```bash
# Set the application name (required)
cmake -DTORQUE_APP_NAME="MyGame" .

# Optional: Set template (defaults to BaseGame)
cmake -DTORQUE_TEMPLATE="BaseGame" .

# Optional: Set script extension (defaults to tscript)
cmake -DTORQUE_SCRIPT_EXTENSION="tscript" .
```

### Building
```bash
# Configure and build
cmake --build . --config Release

# Multi-core build (Windows)
cmake --build . --config Release --parallel
```

### Utility Scripts (Windows)
- `cleanShaders.bat` - Clean compiled shaders
- `DeleteCachedDTSs.bat` - Remove cached 3D model files
- `DeleteDSOs.bat` - Remove compiled script objects
- `DeletePrefs.bat` - Reset preferences

## Project Structure Requirements
- Projects must be created in `My Projects/[APP_NAME]/`
- Game executable outputs to `My Projects/[APP_NAME]/game/`
- Engine source remains in `Engine/source/`
- Templates available in `Templates/` directory