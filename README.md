# Rye-Raylib: Games and Graphics with Rye Language

Rye-Raylib brings the power of [raylib](https://www.raylib.com/) graphics library to the [Rye programming language](https://ryelang.org/). Build cross-platform games, visualizations, and graphics applications with Rye's expressive syntax and raylib's simple yet powerful API.

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

## Resources

- **[Rye Language](https://github.com/refaktor/rye)** - The core Rye language
- **[Rye Website](https://ryelang.org/)** - Documentation and tutorials
- **[raylib](https://www.raylib.com/)** - raylib official website
- **[raylib Cheatsheet](https://www.raylib.com/cheatsheet/cheatsheet.html)** - Quick reference for raylib functions
- **[raylib-go](https://github.com/gen2brain/raylib-go)** - Go bindings for raylib
- **[Reddit Community](https://reddit.com/r/ryelang/)** - Join the discussion

## License

This project is open source under the Apache License 2.0. See the [LICENSE](LICENSE) file for details.
