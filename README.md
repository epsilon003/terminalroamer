# Console Ray Casting Engine

A real-time 3D ray casting engine rendered entirely in the Windows console using ASCII characters. This project demonstrates fundamental 3D graphics techniques using only character-based rendering.

## Overview

This is a simple first-person 3D maze renderer that uses ray casting to create a pseudo-3D perspective view in a console window. The engine casts rays from the player's position to determine wall distances and renders walls with distance-based shading, creating an immersive retro gaming experience reminiscent of early games like Wolfenstein 3D.

## Features

- **Real-time 3D rendering** in a console window (120x40 characters)
- **Ray casting engine** with adjustable field of view
- **Distance-based shading** for depth perception using ASCII characters
- **Wall boundary detection** for enhanced visual detail
- **Collision detection** prevents walking through walls
- **Mini-map overlay** shows player position and maze layout
- **Performance display** showing FPS and player coordinates

## Controls

- **W** - Move forward
- **S** - Move backward
- **A** - Rotate counter-clockwise (left)
- **D** - Rotate clockwise (right)

## Technical Details

### Rendering
- Screen resolution: 120 columns × 40 rows
- Map size: 16 × 16 tiles
- Field of view: π/4 radians (45 degrees)
- Maximum render distance: 16 units
- Shading levels: 4 distance-based intensities using Unicode block characters (█, ▓, ▒, ▒)

### Algorithm
The engine uses a DDA-like ray casting algorithm:
1. For each screen column, cast a ray from the player's position
2. Step along the ray until hitting a wall or reaching maximum distance
3. Calculate wall height based on distance using perspective projection
4. Apply distance-based shading for depth perception
5. Detect wall boundaries by checking corner alignments for enhanced detail

### Performance
The engine uses delta time calculations to ensure consistent movement speed regardless of frame rate. Frame time is calculated using `std::chrono` for precise timing.

## Requirements

- **Platform**: Windows (uses Windows API for console manipulation)
- **Compiler**: C++ compiler with C++11 support or later
- **Libraries**: Windows.h for console buffer operations

## Building

Compile with any standard C++ compiler on Windows:

```bash
g++ raycaster.cpp -o raycaster.exe -std=c++11
```

Or use Visual Studio:
1. Create a new C++ Console Application project
2. Add the source code
3. Build and run (Ctrl+F5)

## How It Works

### Map Representation
The world is represented as a 16×16 grid stored as a string where:
- `#` represents a wall block
- `.` represents empty space

### Ray Casting Process
1. Player has position (x, y) and angle (A)
2. For each screen column, calculate ray angle within FOV
3. March along the ray in small steps (0.1 units)
4. Check if ray intersects a wall block
5. Calculate wall height based on distance to create perspective
6. Apply shading based on distance for depth effect

### Boundary Detection
To add visual detail, the engine detects wall edges by:
- Casting rays from tile corners to the player
- Calculating dot products to determine alignment
- Highlighting boundaries where rays are nearly coincident

## Customization

You can modify these constants to change the behavior:

```cpp
int nScreenWidth = 120;     // Console width
int nScreenHeight = 40;     // Console height
float fFOV = 3.14159f / 4.0f;  // Field of view
float fDepth = 16.0f;       // Render distance
float fSpeed = 5.0f;        // Movement speed
```

## Known Limitations

- Windows-only (uses Windows console API)
- Fixed map size
- No textures (ASCII shading only)
- Simple collision detection
- No sprites or enemies

## Future Enhancements

Possible improvements could include:
- Cross-platform support using ncurses
- Larger or dynamically loaded maps
- Textured walls using ASCII patterns
- Sprite rendering for objects/enemies
- Sound effects
- Menu system

## Credits

This implements a classic ray casting technique popularized by early 3D games. The algorithm is educational and demonstrates core 3D graphics concepts without requiring a GPU or graphics library.

## License

This is educational code provided as-is for learning purposes.
