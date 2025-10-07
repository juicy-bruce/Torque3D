# Project Structure

## Root Directory Layout

```
├── Engine/                 # Core engine code and libraries
│   ├── source/            # Engine C++ source code
│   ├── lib/               # Third-party libraries
│   ├── modules/           # Engine modules
│   └── bin/               # Engine binaries
├── My Projects/           # User game projects
│   └── [ProjectName]/     # Individual game project
│       ├── game/          # Game executable and assets
│       └── source/        # Project-specific C++ code
├── Templates/             # Project templates
│   ├── BaseGame/          # Default game template
│   └── Modules/           # Module templates
├── Tools/                 # Build tools and utilities
│   ├── CMake/             # CMake configuration files
│   ├── dae2dts/           # 3D model conversion tool
│   └── map2dif/           # Map conversion tool
└── .kiro/                 # Kiro IDE configuration
```

## Engine Source Organization

The `Engine/source/` directory is organized by functional areas:

- **core/** - Core engine systems (memory, strings, threading)
- **platform/** - Platform-specific code (Win32, POSIX, etc.)
- **gfx/** - Graphics rendering system
- **gui/** - User interface system
- **console/** - Command console and scripting
- **sim/** - Simulation and game objects
- **T3D/** - 3D game-specific functionality
- **scene/** - Scene management
- **math/** - Mathematical utilities
- **collision/** - Collision detection
- **physics/** - Physics simulation
- **sfx/** - Sound effects system
- **materials/** - Material system
- **lighting/** - Lighting system
- **terrain/** - Terrain rendering
- **forest/** - Vegetation system
- **postFx/** - Post-processing effects

## Project Creation Pattern

New projects follow this structure:
1. Created in `My Projects/[ProjectName]/`
2. Based on templates from `Templates/`
3. Game executable built to `[ProjectName]/game/`
4. Project-specific source in `[ProjectName]/source/`
5. Engine remains separate and shared

## File Naming Conventions

- **C++ files**: `.cpp` and `.h` extensions
- **TorqueScript files**: `.tscript` extension (configurable)
- **CMake files**: `CMakeLists.txt` and `.cmake` extensions
- **Batch scripts**: `.bat` (Windows), `.command` (macOS)

## Module System

Modules can be:
- Engine modules in `Engine/modules/`
- Template modules in `Templates/Modules/`
- Project-specific modules in project directories