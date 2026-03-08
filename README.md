# Rye-Raylib: Game and Graphics Programming with Rye Language

Rye-Raylib brings the power of [raylib](https://www.raylib.com/) graphics library to the [Rye programming language](https://ryelang.org/). Build cross-platform games, visualizations, and graphics applications with Rye's expressive syntax and raylib's simple yet powerful API.

### Download

Download pre-built binaries from [GitHub Releases](https://github.com/refaktor/rye-raylib/releases/latest):
* **Linux**: `rye-raylib-linux-amd64.tar.gz`
* **macOS**: `rye-raylib-macos-amd64.tar.gz`
* **Windows**: `rye-raylib.exe`

### Building from Source

You need [Go](https://go.dev/) installed on your system, along with raylib development dependencies.

```bash
# Clone the repository
git clone https://github.com/refaktor/rye-raylib.git
cd rye-raylib

# Generate bindings (if needed)
go tool ryegen

# Build the project
go build

# Run an example
./rye-raylib examples/ball.rye
```

## Example Applications

### Hello World

```rye
; Basic raylib window
rl: import\go "raylib"

rl/init-window 600 450 "raylib - Hello from Rye!"
rl/set-target-fps 60

while { not rl/window-should-close } {
    rl/begin-drawing
    rl/clear-background rl/ray-white?
    rl/draw-text "Ryelang + Raylib <3" 190 200 20 rl/red?
    rl/end-drawing
}

rl/close-window
```

### Bouncing Ball

```rye
; Bouncing ball animation
rl: import\go "raylib"

screen-width: 800
screen-height: 600

var 'x 400.0
var 'y 300.0
var 'dx 5.0
var 'dy 3.0
radius: 20.0

rl/init-window screen-width screen-height "Bouncing Ball - Rye + Raylib"
rl/set-target-fps 60

while { not rl/window-should-close } {
    ; Update position
    change! x + dx 'x
    change! y + dy 'y

    ; Bounce off walls
    if x < radius { change! negate dx 'dx }
    if x > ( screen-width - radius ) { change! negate dx 'dx }
    if y < radius { change! negate dy 'dy }
    if y > ( screen-height - radius ) { change! negate dy 'dy }

    ; Draw
    rl/begin-drawing
    rl/clear-background rl/ray-white?
    rl/draw-circle x .integer y .integer radius rl/red?
    rl/draw-fps 10 10
    rl/end-drawing
}

rl/close-window
```

### Snake Game

The repository includes a complete Snake game implementation in `examples/snake.rye` demonstrating:
- Game state management
- Keyboard input handling
- Collision detection
- Score tracking
- Game over and restart logic

## Features

### Graphics Primitives
- Shapes: circles, rectangles, lines, triangles, polygons
- Text rendering with customizable fonts
- Texture and image support
- Color manipulation

### Input Handling
- Keyboard input (key press, key down, key up)
- Mouse input (position, buttons, wheel)
- Gamepad support

### Window Management
- Window creation and configuration
- Fullscreen toggle
- FPS control and display
- Screen dimensions

### Audio (via raylib)
- Sound loading and playback
- Music streaming
- Volume control

## Interactive Development

Start the Rye console for interactive graphics development:

```bash
./rye-raylib
```

```rye
; Quick graphics demo in the console
rye> rl: import\go "raylib"
rye> rl/init-window 400 300 "Quick Demo"
rye> rl/set-target-fps 60
rye> loop 100 { rl/begin-drawing rl/clear-background rl/blue? rl/end-drawing }
rye> rl/close-window
```

## Cross Generation

With ryegen, bindings are generated per OS and architecture. To cross-generate:

```bash
# Generate for different platforms
go tool ryegen -goarch amd64 -goos linux
go tool ryegen -goarch amd64 -goos darwin
go tool ryegen -goarch amd64 -goos windows
```

## Raylib API Coverage

Rye-Raylib provides access to raylib's core modules:
- **core**: Window, input, timing
- **shapes**: 2D shape drawing
- **textures**: Image/texture loading and drawing
- **text**: Font loading and text drawing
- **models**: 3D model loading and rendering
- **audio**: Sound and music playback

Functions are converted to kebab-case following Rye conventions:
- `InitWindow` → `init-window`
- `DrawCircle` → `draw-circle`
- `IsKeyPressed` → `is-key-pressed`
- `ClearBackground` → `clear-background`

## Resources

- **[Rye Language](https://github.com/refaktor/rye)** - The core Rye language
- **[Rye Website](https://ryelang.org/)** - Documentation and tutorials
- **[raylib](https://www.raylib.com/)** - raylib official website
- **[raylib Cheatsheet](https://www.raylib.com/cheatsheet/cheatsheet.html)** - Quick reference for raylib functions
- **[raylib-go](https://github.com/gen2brain/raylib-go)** - Go bindings for raylib
- **[Reddit Community](https://reddit.com/r/ryelang/)** - Join the discussion

## What is Rye?

Rye is a high-level, dynamic programming language inspired by Rebol, Factor, and Go. It emphasizes:
- **Expressive Syntax**: Clean, readable code that's easy to write and understand
- **Interactive Development**: REPL-driven programming with live feedback
- **Go Integration**: Easy access to Go libraries and embedding in Go applications
- **Cross-platform**: Build applications that run on Windows, macOS, and Linux

## What is raylib?

raylib is a simple and easy-to-use library to enjoy videogames programming. It's:
- **Cross-platform**: Works on Windows, Linux, macOS, and more
- **No dependencies**: Self-contained, minimal setup required
- **OpenGL based**: Hardware-accelerated graphics
- **Game-focused**: Designed for game development from the ground up

## Contributing

Contributions are welcome! Please feel free to submit issues, feature requests, or pull requests on GitHub.

## License

This project is open source under the Apache License 2.0. See the [LICENSE](LICENSE) file for details.
