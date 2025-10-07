# Design Document

## Overview

The Interactive Map Spawn System extends the existing MapViewDlg GUI to provide tactical spawn point selection through interactive buttons overlaid on the map. The system leverages the existing GuiMapSelectorCtrl infrastructure while adding a new layer of GUI buttons that represent SpawnSphere locations. The design integrates seamlessly with the current team-based capture point system and spawn selection mechanism.

## Architecture

### Core Components

1. **MapSpawnButtonManager** - A new TorqueScript class responsible for managing spawn point buttons
2. **Enhanced MapViewDlg** - Extended GUI container with spawn button overlay
3. **SpawnButton Controls** - Dynamic GuiButtonCtrl instances representing spawn points
4. **Team Color System** - Dynamic color management based on team ownership
5. **Integration Layer** - Interfaces with existing spawn selection and capture point systems

### System Flow

```
MapViewDlg Opens → Query SpawnSpheres → Create Buttons → Position on Map → Handle Clicks → Spawn Player
                                    ↓
                              Update Colors ← Monitor Team Changes ← Capture Point System
```

## Components and Interfaces

### MapSpawnButtonManager Class

**Purpose**: Central manager for all spawn point button operations

**Key Methods**:
- `initializeSpawnButtons()` - Query SpawnSpheres and create initial buttons
- `updateButtonColors()` - Refresh button colors based on team ownership
- `positionButton(%spawnSphere, %button)` - Convert world coordinates to map coordinates
- `onSpawnButtonClick(%button, %spawnIndex)` - Handle button click events
- `clearSpawnButtons()` - Clean up buttons when map closes

**Properties**:
- `spawnButtons[]` - Array of created button controls
- `spawnSpheres[]` - Array of corresponding SpawnSphere objects
- `buttonCount` - Number of active buttons

### Enhanced MapViewDlg GUI Structure

```
MapViewDlg (GuiControl)
├── GuiContainer (existing map container)
│   ├── GuiBitmapCtrl (existing background)
│   ├── GuiMapSelectorCtrl (existing MapViewer)
│   └── GuiContainer (new spawn button overlay)
│       ├── GuiButtonCtrl (spawn button 1)
│       ├── GuiButtonCtrl (spawn button 2)
│       └── ... (dynamic spawn buttons)
```

### SpawnButton Control Specification

**Control Type**: GuiButtonCtrl
**Size**: 20x20 pixels (configurable)
**Profile**: Custom profile with team-based coloring
**Text**: Spawn point identifier or empty
**Command**: `MapSpawnButtonManager.onSpawnButtonClick(%this, %index);`

### Team Color System

**Color Mapping**:
- Team 1 (Friendly): Blue (#0066FF)
- Team 2 (Enemy): Red (#FF0000) 
- Neutral/Unowned: Gray (#808080)

**Implementation**: Dynamic profile switching or bitmap modulation

## Data Models

### SpawnButtonData Structure
```torquescript
// Data stored in arrays indexed by button ID
%manager.spawnButtons[%i] = %buttonControl;
%manager.spawnSpheres[%i] = %spawnSphere;
%manager.worldPositions[%i] = %worldPosition;
%manager.mapPositions[%i] = %mapPosition;
%manager.teamOwnership[%i] = %teamValue; // 0=neutral, 1=team1, 2=team2
%manager.isAvailable[%i] = %available;
%manager.spawnIndices[%i] = %spawnIndex;
```

### Coordinate Conversion System
```torquescript
// World to Map coordinate conversion
function MapSpawnButtonManager::convertWorldToMap(%this, %worldPos)
{
   %missionArea = MissionArea.getServerObject().getArea();
   %mapExtent = MapViewer.getExtent();
   
   %mapX = (%worldPos.x - %missionArea.point.x) / %missionArea.extent.x * %mapExtent.x;
   %mapY = (%worldPos.y - %missionArea.point.y) / %missionArea.extent.y * %mapExtent.y;
   
   // Account for map container offset
   %containerPos = MapViewer.getPosition();
   %finalX = %mapX + %containerPos.x;
   %finalY = %mapY + %containerPos.y;
   
   return %finalX SPC %finalY;
}
```

## Error Handling

### Spawn Point Validation
- Verify SpawnSphere objects exist and are valid
- Check team ownership before allowing spawn
- Validate spawn cooldown timers
- Handle cases where spawn points become unavailable

### GUI Error Recovery
- Graceful handling of missing GUI containers
- Recovery from button creation failures
- Cleanup of orphaned button controls
- Fallback to existing spawn selection system

### Network Error Handling
- Timeout handling for spawn selection commands
- Retry logic for failed spawn attempts
- Client-server synchronization validation

### Multiplayer Client-Server Synchronization

**Purpose**: Ensure the map spawn system works correctly for clients in multiplayer games

**Components**:
1. **Server-side Data Synchronization** - AFPSKRadar module server scripts that send MissionArea and spawn point data to clients
2. **Client-side MissionArea Creation** - Create client-side MissionArea objects when server data is received
3. **Module Integration** - Move synchronization functions from TeamHQGame to AFPSKRadar module for reusability

**Data Flow**:
```
Server (AFPSKRadar) → Send MissionArea Data → Client Creates MissionArea → Map System Functions
                   → Send Spawn Point Data → Client Stores Data → Button Manager Uses Data
```

## Testing Strategy

### Unit Testing
1. **Coordinate Conversion Tests**
   - Verify accurate world-to-map coordinate transformation
   - Test edge cases (map boundaries, zero-size areas)
   - Validate scaling with different map sizes

2. **Button Management Tests**
   - Test button creation and destruction
   - Verify proper cleanup on map close
   - Test button positioning accuracy

3. **Team Color Tests**
   - Verify correct color assignment based on team ownership
   - Test color updates when ownership changes
   - Validate color consistency across different scenarios

4. **Multiplayer Synchronization Tests**
   - Test MissionArea data transmission from server to client
   - Verify client-side MissionArea object creation
   - Test coordinate conversion with synchronized data

### Integration Testing
1. **Spawn System Integration**
   - Test integration with existing serverCmdSelectSpawn
   - Verify spawn point availability checking
   - Test spawn cooldown integration

2. **Capture Point Integration**
   - Test real-time color updates when capture points change
   - Verify team ownership propagation to spawn points
   - Test multiple simultaneous ownership changes

3. **GUI Integration**
   - Test MapViewDlg opening/closing with buttons
   - Verify button positioning with different map sizes
   - Test interaction with existing map controls

4. **Multiplayer Integration**
   - Test system functionality when client joins multiplayer game
   - Verify data synchronization between server and multiple clients
   - Test system behavior when server data is delayed or missing

### User Acceptance Testing
1. **Usability Testing**
   - Verify buttons are easily clickable
   - Test visual clarity of team colors
   - Validate intuitive spawn point selection

2. **Performance Testing**
   - Test with maximum number of spawn points
   - Verify smooth color updates during gameplay
   - Test memory usage with long gaming sessions

3. **Edge Case Testing**
   - Test with no available spawn points
   - Test with overlapping spawn point positions
   - Test rapid team ownership changes

4. **Multiplayer Testing**
   - Test system with multiple clients connecting and disconnecting
   - Verify system works correctly for both host and client players
   - Test system behavior with network latency and packet loss

## Implementation Notes

### TorqueScript Considerations
- Use existing GUI profile system for consistent styling
- Leverage GuiContainer's automatic layout management
- Implement proper object cleanup to prevent memory leaks
- Use schedule() for deferred operations when needed

### Performance Optimizations
- Cache coordinate conversions when possible
- Batch color updates to minimize GUI refreshes
- Use object pooling for frequently created/destroyed buttons
- Implement dirty flag system for selective updates

### Compatibility Requirements
- Maintain backward compatibility with existing spawn system
- Ensure graceful degradation if new features fail
- Support existing key bindings and commands
- Preserve current MapViewDlg functionality