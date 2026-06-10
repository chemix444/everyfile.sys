# everyfile.sys

A browser recreation of [PortalRunner's "This Flash Drive has Literally Every File"](https://www.youtube.com/watch?v=w6rkhvdAqHU), built as a single HTML file.

The original video shows a microcontroller pretending to be a USB drive over MTP, generating every possible file on the fly. This page simulates the same logic in your browser: nothing is stored, the folder path *is* the file.

## How to use

- Open the [live demo](https://chemix444.github.io/everyfile.sys/), **or**
- Download `index.html` and open it in any modern browser. No build steps, no dependencies.

## What it does

- **Infinite explorer** with 4,900 generated folders per level (70-symbol alphabet, 2-character names, the optimum from the video)
- **Path-as-cipher decoding**: your route through the folders is read as one big base-4,900 number and converted to base-256 bytes to produce the file at that path
- **Leading-zero fix**: uses bijective numeration (the same offset trick from the video) so every byte sequence, including null bytes, maps to exactly one path with no duplicates or gaps
- **LOCATE.EXE**: type any text and it computes the exact path where that file "already exists" on the drive, then jumps there and decodes it back
- Text and hex views for file contents, plus a README window explaining the math

## How it works (short version)

1. Each folder at a given level is a digit from 0 to 4,899
2. The full path is treated as one giant base-4,900 integer (BigInt)
3. That integer is rewritten in base 256, where each digit is one byte of the file
4. Finding a file is just the same conversion run backwards

## Limitations

- The locator caps input at 4 KB, since the printed path gets absurdly long past that. The math itself has no limit
- This is a simulation, not a USB device. For the real hardware build, see PortalRunner's repo linked in the video description

## Credits

Concept and original implementation by [PortalRunner](https://www.youtube.com/@PortalRunner). This is a fan recreation for fun and learning.
