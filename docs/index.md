---
hide:
  - navigation
---

<div class="hero" markdown>

# HLSLens

Custom HLSL post-processing for Unreal Engine 5. Lens flares, bloom, halation, tonemapping and more, all configured from a single post-process volume.

<!-- TODO: replace the Fab link with your product page -->
[Get started](installation.md){ .md-button .md-button--primary }
[View on Fab](https://www.fab.com/){ .md-button }

</div>

## Overview

HLSLens is a post-processing plugin for Unreal Engine 5. It adds its own post-process volume, the **Advanced Post Process Volume**, and replaces parts of the engine's post-processing with custom effects written in HLSL.

All settings live in the volume's **Details** panel, so working with HLSLens feels like working with the engine's own Post Process Volume. You do not need `.ini` files or console variables to configure the effects.

!!! success "Non-destructive"
    No engine files are deleted or modified.

## Key features

<div class="grid cards" markdown>

-   :material-flare: **[Lens flares](lens-flares.md)**

    Halo, glare and ghosts, each adjustable on its own. Glare comes in two styles: Three Streaks and Directional Blur.

-   :material-white-balance-sunny: **[Bloom](bloom.md)**

    A Kawase-blur bloom designed to avoid the banding the engine's bloom can show in its falloff, with an optional brightness threshold.

-   :material-filmstrip: **[Halation](halation.md)**

    A soft glow that spreads from the brightest highlights.

-   :material-chart-bell-curve-cumulative: **Tonemapper**

    The engine's ACES tonemapper or the HLSLens Perceptual tonemapper, which keeps emissive lights closer to their true color. Brightness and hue controls for 12 color channels.

-   :material-looks: **Chromatic aberration**

    A Basic mode and a Dynamic Blurring mode with depth-based intensity, custom spectral colors and fringe blur.

-   :material-grain: **Film grain**

    Procedural or texture-based grain with optional chromatic grain.

-   :material-camera-iris: **Lens distortion**

    Barrel and pincushion distortion.

-   :material-circle-opacity: **Vignette and damage indicators**

    A vignette with shape and falloff controls, plus a directional damage indicator driven by a world-space hit location (singleplayer only).

-   :material-palette-swatch: **LUT blending**

    Blend LUTs and color-correction settings by scene depth, a custom mask or time of day.

-   :material-bug-outline: **Debug tools**

    On-screen overlays for the Perceptual tonemapper curve and for time-of-day blending.

</div>

## Good to know

**A volume is required.**
Without an Advanced Post Process Volume in your level, the custom effects have nothing to read their settings from.

**Most optional effects are off by default.**
Film Grain, Chromatic Aberration and Lens Distortion start at intensity `0.0`.

**The Perceptual tonemapper changes your look.**
It shows emissive colors more accurately, so you will likely need to adjust some light colors. ACES remains available and works with all of the HLSLens effects.

**Performance.**
HLSLens costs slightly more GPU time than the engine's default post-processing. See the Performance section for results.

**Some features are left untouched.**
Motion blur and depth of field are not changed by HLSLens. Anti-aliasing, global illumination, reflections and so on are not touched either. They work the same with HLSLens as they do with the engine's post-processing.
