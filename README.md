# RetroPak V8

### *"I heard you like Quake"*

**RetroPak** is a single-file, zero-install, runs-anywhere-with-a-browser tool for cracking open, browsing, editing, and repacking Quake-era game archives. We're talking one HTML file. Drag a `.pak` onto it and you're in.

No server. No Node. No Python. No Electron wrapper. Just double-click `RetroPakV8.html` and go.

It was built using **Antigravity** with **Gemini 3.5** and **GLM 5.2 (Z.AI)** doing the heavy lifting on the code generation side.

---

## What's New in V8 / V7

### Quake 3 Arena level support (IBSP v46)
- **Bezier Patch Tessellation**: Real-time quadratic Bezier curve patch generation for rounded columns, pipes, and arches.
- **Multi-pass Q3 Shader Pipeline**: Wrote a complete parser and multi-stage WebGL renderer for Quake 3 shader scripts, supporting texture scrolling, scaling, rotating, stretching, environment mapping, `rgbGen`, `alphaFunc`, and complex `blendFunc` blend equations.
- **PK3 Archive support**: Fully unzip and extract assets from Quake 3 `.pk3` zip-inflated mod archives.

### Advanced Lightmap Rendering (Quake 1, 2, & Half-Life)
- **Edge-Pixel Replication (Clamping)**: Fixed the notorious grey seams between brushes on Quake 1 maps by copying texture data into a 1-pixel padding gutter and clamping lookup coordinates inside the WebGL atlas writer, eliminating bilinear interpolation bleeding.
- **Quake 2 Colored Overbrighting**: Restored missing overbrighting multiplier of `2.0x` for non-Q3 maps inside the fragment shader, ensuring Quake 2's colored lights are displayed at full intensity.
- **Explicit Binding**: Optimised lightmap texture state management to bind once-per-frame, eliminating misplaced textures during map changes.

### Expanded Format Coverage
- **MD3 Model Support**: Quake 3 Arena's multi-mesh attachment-tag model format with vertex animation.
- **GoldSrc MDL & IQM**: Real-time Linear Blend Skinning (LBS) skeletal animation for Half-Life `.mdl`, InterQuake Model `.iqm`, and Doom 3 `.md5`.
- **Multiple Workspaces**: Load multiple PAK, PK3, and WAD files concurrently in a single virtual tree explorer.

---

## How to Use It

1. **Double-click `RetroPakV8.html`** in your file browser.
2. **Load an archive.** Either:
   - Click the dropzone and select a `.pak`, `.pk3`, or `.wad` file.
   - Drag-and-drop an archive straight onto the browser window.
3. **Browse.** Navigate the folder tree on the left. Click files to preview them:
   - 3D Models (.mdl, .md2, .md3, .iqm, .md5mesh) spin up in a real-time WebGL viewer with skeletal animation, scrubbing, and frame rates.
   - 3D Maps (.bsp) render fully with fly/orbit camera controls.
   - Images (.pcx, .tga, .wal, .lmp, sprites) decode and display with a pixelated zoom slider (1x to 16x).
   - Audio (.wav) files play inline with a custom audio player.
   - Text lumps (.ent, .cfg, .qc, .txt) open in an editor with line numbers.
4. **Edit & Repack.** Rename, delete, or import assets. Click "Save" to recompile the virtual archive buffer back into a standard PAK file and download it.

---

## Full File Compatibility List

### Archive Formats

| Format | Extension | Read | Write | Engine / Games |
|--------|-----------|:----:|:-----:|----------------|
| Quake PAK | `.pak` | Yes | Yes | Quake 1, Quake 2, and derivatives |
| Quake 3 PK3 | `.pk3` | Yes | No | Quake 3 Arena, Return to Castle Wolfenstein |
| Half-Life WAD | `.wad` | Yes | No | GoldSrc, WAD2 (Quake 1) / WAD3 (Half-Life) |

### 3D Model Formats

| Format | Extension | Preview | Textures | Animation | Engine / Origin |
|--------|-----------|:-------:|:--------:|:---------:|-----------------|
| Quake 1 MDL | `.mdl` | Yes | Embedded | Vertex morphs | Quake |
| Half-Life MDL | `.mdl` | Yes | Embedded | Skeletal (LBS) | GoldSrc |
| Quake 2 MD2 | `.md2` | Yes | External | Vertex morphs | Quake II |
| Quake 3 MD3 | `.md3` | Yes | External | Vertex morphs | Quake III Arena |
| InterQuake Model | `.iqm` | Yes | External | Skeletal (LBS) | Sauerbraten / FTE |
| Doom 3 MD5 | `.md5mesh` | Yes | External | Skeletal (LBS) | Doom 3 / Quake Remaster |

### 3D Map Formats

| Format | Extension | Preview | Textures | Lighting | Special Features |
|--------|-----------|:-------:|:--------:|:--------:|------------------|
| Quake 1 BSP | `.bsp` | Yes | Paired WAD | Lightmaps | Warp liquid, scroll sky |
| Quake 2 BSP | `.bsp` | Yes | Embedded | Lightmaps | Full colored lights, overbright |
| Half-Life BSP | `.bsp` | Yes | Embedded / WAD | Lightmaps | StudioModel entities, transparency |
| Quake 3 BSP | `.bsp` | Yes | PK3 | Lightmaps / Shaders | Bezier patches, multi-stage shaders |

---

## Credits and References

### Format Specifications and Reference Documentation

- **Quake Source & Quake 2 Source (id Software)**: PAK/PK3 archive layout, MDL/MD2 format specs, BSP structure. [github.com/id-Software/Quake](https://github.com/id-Software/Quake) / [github.com/id-Software/Quake-2](https://github.com/id-Software/Quake-2)
- **Quake III Arena Source (id Software)**: Foundation for Bezier calculations and shader parser state logic. [github.com/id-Software/Quake-III-Arena](https://github.com/id-Software/Quake-III-Arena)
- **Inter-Quake Model SDK (Lee Salzman & Wouter van Oortmerssen)**: IQM skeletal loading code, joints matrix transform references. [github.com/lsalzman/iqm](https://github.com/lsalzman/iqm)
- **Half-Life 1 SDK (Valve)**: GoldSrc MDL v10 structures. [github.com/ValveSoftware/halflife](https://github.com/ValveSoftware/halflife)
- **Brandon Jones (toji)**: Original WebGL Quake 3 renderer. [github.com/toji/webgl-quake3](https://github.com/toji/webgl-quake3)
- **sairuk & passiomatic**: Extensions to WebGL BSP render paths. [github.com/sairuk/oa-webgl-browser](https://github.com/sairuk/oa-webgl-browser) / [github.com/passiomatic/elm-quake3-renderer](https://github.com/passiomatic/elm-quake3-renderer)

---

## License

This is a personal hobby project. Modify it, learn from it, and hack it to your liking! If you include it in something larger, please credit Antigravity, Gemini 3.5, GLM 5.2 (Z.AI), and TDA317.

*Now double-click and open a map!*
