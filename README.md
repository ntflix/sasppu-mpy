# SASPPU Module for MicroPython Documentation

The **sasppu** module provides hardware-accelerated graphics routines and state objects, enabling efficient manipulation of sprites, backgrounds, colour math, and more using MicroPython.

> Access advanced graphics hardware operations with minimal latency with state objects (Background, Sprite, etc.), low-level memory access (OAM, maps, HDMA), and fast drawing functions.
>
> For additional details, refer to the inline docstrings within the `.pyi` file.

This documentation covers the API, including state objects, drawing functions, low-level hardware access, and utility functions.

---

## Overview

The `sasppu` module exposes a set of classes and functions to allow direct control of graphics hardware:

### State Objects

Manage hardware states for backgrounds and sprites.

### Drawing Functions

Fast blitting, copying, filling, and text drawing routines.

### Hardware Objects

Direct access to OAM, background tile maps (MAP), and HDMA tables.

### Colour Math Helpers

Functions and macros for composing and manipulating colour values.

---

## Classes and State Objects

### ImageCode

The `ImageCode` class provides constants for image operation results:

- `ImageCode.Success`: Operation succeeded.
- `ImageCode.TooWide`: Image width exceeds the allowed limit.
- `ImageCode.TooTall`: Image height exceeds the allowed limit.
- `ImageCode.InvalidBitdepth`: Invalid bit depth for the operation.

---

## Predefined Colours

The module provides several predefined colour constants:

- `TRANSPARENT_BLACK`: Transparent black colour.
- `OPAQUE_BLACK`: Opaque black colour.
- `RED`: Red colour.
- `GREEN`: Green colour.
- `BLUE`: Blue colour.
- `WHITE`: White colour.

---

## Drawing and Graphics Operations

### Sprite Functions

The following functions are available for sprite manipulation:

`copy_sprite(dst_x, dst_y, width, height, src_x, src_y, double_size)`

- Copies a rectangular region from one sprite to another.

`copy_sprite_transparent(...)`

- Same as `copy_sprite`, but treats a specific colour as transparent.

`blit_sprite(x, y, width, height, double_size, data)`

- Blits raw sprite data to the screen.

`blit_sprite_transparent(...)`

- Same as `blit_sprite`, but treats a specific colour as transparent.

`paletted_sprite(x, y, width, height, double_size, data, palette, bitdepth)`

- Draws a sprite using a palette and specified bit depth.

`paletted_sprite_transparent(...)`

- Same as `paletted_sprite`, but treats a specific colour as transparent.

`compressed_sprite(x, y, width, height, double_size, data, palette, bitdepth)`

- Draws a compressed sprite using a palette and specified bit depth.

`compressed_sprite_transparent(...)`

- Same as `compressed_sprite`, but treats a specific colour as transparent.

`fill_sprite(x, y, width, height, colour)`

- Fills a rectangular region of a sprite with a specific colour.

`draw_text_sprite(x, y, colour, line_width, newline_height, double_size, text)`

- Draws text onto a sprite.

`draw_text_next_sprite(...)`

- Continues drawing text on the next line of a sprite.

---

### Background Functions

The following functions are available for background manipulation:

`copy_background(dst_x, dst_y, width, height, src_x, src_y, double_size)`

- Copies a rectangular region from one background to another.

`copy_background_transparent(...)`

- Same as `copy_background`, but treats a specific colour as transparent.

`blit_background(x, y, width, height, double_size, data)`

- Blits raw background data to the screen.

`blit_background_transparent(...)`

- Same as `blit_background`, but treats a specific colour as transparent.

`paletted_background(x, y, width, height, double_size, data, palette, bitdepth)`

- Draws a background using a palette and specified bit depth.

`paletted_background_transparent(...)`

- Same as `paletted_background`, but treats a specific colour as transparent.

`compressed_background(x, y, width, height, double_size, data, palette, bitdepth)`

- Draws a compressed background using a palette and specified bit depth.

`compressed_background_transparent(...)`

- Same as `compressed_background`, but treats a specific colour as transparent.

`fill_background(x, y, width, height, colour)`

- Fills a rectangular region of a background with a specific colour.

`draw_text_background(x, y, colour, line_width, newline_height, double_size, text)`

- Draws text onto a background.

`draw_text_next_background(...)`

- Continues drawing text on the next line of a background.

---

## Colour Math Macros and Helpers

The module provides several helper functions to create and manipulate colour values:

`grey555(g)`

- Creates a grayscale colour in 15-bit RGB format.

`grey555_cmath(g)`

- Creates a grayscale colour in 15-bit RGB format with colour math applied.

`rgb555(r, g, b)`

- Converts red, green, and blue channels to a 15-bit RGB value.

`rgb555_cmath(r, g, b)`

- Same as `rgb555`, but with colour math applied.

`rgb888(r, g, b)`

- Converts red, green, and blue channels to a 24-bit RGB value.

`rgb888_cmath(r, g, b)`

- Same as `rgb888`, but with colour math applied.

`mul_rgb555(r, g, b, mul)`

- Multiplies the red, green, and blue channels of a 15-bit RGB colour by a multiplier.

`mul_col(col, mul)`

- Multiplies an entire colour value by a multiplier.

`r_channel(col)`

- Extracts the red channel from a colour.

`g_channel(col)`

- Extracts the green channel from a colour.

`b_channel(col)`

- Extracts the blue channel from a colour.

`cmath_channel(col)`

- Extracts the "colour math" portion of a colour.

---

## Utility Functions

`get_text_size(line_width, newline_height, double_size, text)`

- Returns a tuple `(width, height)` indicating the dimensions needed to display the text.

`gfx_reset()`

- Resets the graphics hardware to its initial state.

---

## Constants and Predefined Values

The module provides several constants for easy use:

### Image Codes

- `ImageCode.Success`
- `ImageCode.TooWide`
- `ImageCode.TooTall`
- `ImageCode.InvalidBitdepth`

### Predefined Colours

- `TRANSPARENT_BLACK`
- `OPAQUE_BLACK`
- `RED`
- `GREEN`
- `BLUE`
- `WHITE`

---

## Usage Examples

### Example 1 – Drawing a Sprite

```python
from sasppu import Sprite, draw_text_sprite, IC_SUCCESS

spr = Sprite()
spr.x = 50
spr.y = 60
spr.width = 32
spr.height = 32
spr.bind(3)  # Bind sprite to OAM index 3

result = draw_text_sprite(0, 0, 31, 100, "Hello World", True)
if result == IC_SUCCESS:
    print("Text drawn successfully!")
```

### Example 2 – Drawing Text on a Background

```python
from sasppu import Background, draw_text_background

bg = Background()
bg.x = 0
bg.y = 0
bg.bind(1)  # Bind to BG1

res = draw_text_background(0, 0, 31, 120, "Hello, SASPPU!", False)
if res == sasppu.IC_SUCCESS:
    print("Text drawn on BG successfully!")
```
