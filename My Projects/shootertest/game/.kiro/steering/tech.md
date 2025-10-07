# Technology Stack

## Engine & Framework
- **Torque3D Engine**: Core 3D game engine
- **TorqueScript**: Primary scripting language (`.tscript` files)
- **Module System**: Component-based architecture using `.module` definition files

## Build System & Executables
- **Debug Build**: `shootertest_DEBUG.exe` - Development version with debug symbols
- **Release Build**: `shootertest.exe` - Optimized production version
- **Project File**: `shootertest.torsion` - Torsion IDE project configuration

## Dependencies & Libraries
- **DirectX**: D3DCompiler_47.dll for Windows graphics
- **OpenAL**: Audio system (OpenAL32.dll, OpenAL32d.dll for debug)
- **SDL2**: Cross-platform development library (SDL2.dll, SDL2d.dll for debug)

## Common Commands

### Running the Game
```cmd
# Debug version
shootertest_DEBUG.exe

# Release version  
shootertest.exe

# Dedicated server mode
shootertest.exe -dedicated

# Compile all scripts
shootertest.exe -compileAll

# Compile tools only
shootertest.exe -compileTools
```

### Development Workflow
- Scripts are compiled at runtime or via command-line flags
- Module system automatically scans and loads components
- Settings stored in XML files (`core/settings.xml`, `tools/settings.xml`)
- Preferences saved to `clientPrefs.tscript` in user directory

## File Extensions
- `.tscript` - TorqueScript source files
- `.module` - Module definition files
- `.gui` - GUI layout files  
- `.taml` - Asset definition files
- `.xml` - Configuration files