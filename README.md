# GRAM: Generate Resource/Assets Module

Gram is a lightweight Zig library with a single purpose: generating a Zig module for
your resources or assets. It's so lightweight in fact, that it exists entirely within
the `build.zig`.

[![Static Badge](https://img.shields.io/badge/v0.16(stable)-orange?logo=Zig&logoColor=Orange&label=Zig&labelColor=Orange)](https://ziglang.org/download/)
[![Static Badge](https://img.shields.io/badge/MIT-silver?label=License)](https://github.com/00JCIV00/cova/blob/main/LICENSE)


## Installation

1. Install `gram` to your project.

```shell
zig fetch --save git+https://github.com/00jciv00/gram.git
```

2. Import it into your `build.zig`

```zig
// Within your `build.zig`
const gram = @import("gram");
```

## Usage

Assuming a project structure similar to:

```shell
.
├── assets
│   └── fonts
│       ├── summer-fav.ttf
│       ├── super-pixel.ttf
│       ├── supreme-spike.otf
│       └── techno-race-italic.otf
├── build.zig
├── build.zig.zon
└── src
    ├── cli.zig
    ├── game.zig
    ├── main.zig
    └── ui.zig
```

Setup your `build.zig` as follows:

```zig
const std = @import("std");
const gram = @import("gram");

pub fn build(b: *std.Build) void {
    // Target & Optimize
    // ...
    
    // Generate your Assets Module
    const assets = gram.genModule(b, .{});
    
    // Exe Setup
    // ...

    // Add your Assets Module as an Import
    exe.root_module.addImport("assets");
}
```

Access your `assets` Module from your `main.zig`:

```zig
const assets = @import("assets");

pub fn main() void {
    const super_pixel_font = assets.fonts.@"super-pixel.ttf";
}
```

_Note: This will add `assets.zig` to your `assets` directory:_

```shell
.
├── assets
│   ├── assets.zig
│   └── fonts
│       ├── summer-fav.ttf
│       ├── super-pixel.ttf
│       ├── supreme-spike.otf
│       └── techno-race-italic.otf
├── build.zig
├── build.zig.zon
└── src
    ├── cli.zig
    ├── game.zig
    ├── main.zig
    └── ui.zig
```
