# Project Structure

## Root Directory
- **Main Scripts**: `main.tscript`, `main.tscript.in` - Entry points for the application
- **Executables**: `shootertest.exe` (release), `shootertest_DEBUG.exe` (debug)
- **Project Files**: `shootertest.torsion` - Torsion IDE project configuration
- **Dependencies**: DLL files for DirectX, OpenAL, and SDL2

## Core Directory (`/core`)
Engine core functionality and base systems:
- **Module Definition**: `core.module` - Defines core engine module
- **Main Script**: `core.tscript` - Core engine initialization
- **Settings**: `settings.xml` - Core engine configuration
- **Subsystems**:
  - `clientServer/` - Networking and client/server architecture
  - `console/` - Debug console and command system
  - `gameObjects/` - Base game object classes and systems
  - `gui/` - Core GUI framework and controls
  - `lighting/` - Lighting system and shaders
  - `postFX/` - Post-processing effects
  - `rendering/` - Core rendering pipeline
  - `sfx/` - Sound effects and audio system
  - `utility/` - Utility functions and helper classes

## Data Directory (`/data`)
Game content, assets, and gameplay modules:
- **Base Files**: `defaults.tscript`, asset files (`splash.png`, `torque.png`)
- **Gameplay Modules**:
  - `FPSPlayer-main/` - First-person player controller and mechanics
  - `FPSGameplay-master/` - Core FPS gameplay systems
  - `FPSEquipment-main/` - Weapons and equipment systems
  - `TeamHQGameplay/` - Team-based headquarters game mode
  - `inventorySystem-master/` - Item and inventory management
  - `noticeSystem-main/` - UI notification system
  - `DamageModel/` - Damage calculation and health systems
- **Specialized Systems**:
  - `AFPSKRadar/` - Radar and minimap functionality
  - `ExampleModule/` - Template/example module structure
  - `Prototyping/` - Development and testing content
  - `testMaps-main/` - Test levels and maps
- **UI Systems**:
  - `gameUI/` - In-game user interface
  - `UI/` - General UI components and layouts
- **Cache**: `cache/` - Runtime generated and cached files

## Tools Directory (`/tools`)
Development tools and editor functionality:
- **Module Definition**: `tools.module` - Defines tools module
- **Main Scripts**: `main.tscript`, `tools.tscript` - Tools initialization
- **Settings**: `settings.xml` - Editor configuration
- **Core Tools**:
  - `base/` - Base editor functionality
  - `editorCore/` - Core editor systems
  - `editorClasses/` - Editor-specific class definitions
  - `gui/` - Editor GUI framework
  - `guiEditor/` - GUI layout editor
- **Content Editors**:
  - `worldEditor/` - 3D world/level editor
  - `materialEditor/` - Material and shader editor
  - `shapeEditor/` - 3D model editor
  - `particleEditor/` - Particle system editor
  - `forestEditor/` - Vegetation and forest editor
  - `decalEditor/` - Decal placement editor
- **Specialized Editors**:
  - `meshRoadEditor/` - Road creation tools
  - `riverEditor/` - River and water body editor
  - `roadEditor/` - Road network editor
  - `navEditor/` - AI navigation mesh editor
  - `VerveEditor/` - Animation and cutscene editor
  - `VPathEditor/` - Path editing tools
- **Asset Management**:
  - `assetBrowser/` - Asset browsing and management
  - `projectImporter/` - Project import utilities
  - `datablockEditor/` - Datablock editing tools
- **Development Tools**:
  - `debugger/` - Script debugging tools
  - `windowConsole/` - Console window interface
  - `autosave/` - Automatic save functionality
  - `componentEditor/` - Component system editor
  - `convexEditor/` - Collision shape editor
  - `physicsTools/` - Physics debugging and tools
  - `shaderEditor/` - Shader development tools
- **Resources**: `resources/` - Tool-specific assets and resources

## Configuration Files
- **Kiro Settings**: `.kiro/` - IDE-specific configuration and steering rules
- **IDE Configuration**: `.vscode/`, `.idea/` - Editor-specific settings
- **Version Control**: `.git/` - Git repository data
- **Project Settings**: Various `.xml` files for engine and tool configuration

## Module System
The project uses a modular architecture where:
- Each major system has a `.module` file defining its structure
- Modules are automatically discovered and loaded by the engine
- Dependencies between modules are managed through the module system
- Scripts are organized by functionality within each module directory