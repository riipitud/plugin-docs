<p class="eyebrow">Effect</p>

# Lens flares

<p class="lead">A lens flare is what you get when a bright light hits a camera lens.</p>

Modern lenses are a composite of multiple differently shaped glasses that bend light rays toward the sensor. Flares were first seen as defects, and filmmakers used to avoid them. Today they are a look of their own and help an image feel more realistic.

In HLSLens the flares are **procedural**. They are not images, sprites or Niagara effects, and you don't have to place anything in your level. HLSLens looks at the scene, finds the bright pixels and builds the flare out of them, just like the engine does, only with more advanced methods.

<div class="glance" markdown>
Where to find it
:   Post Process Volume → Bloom & Lens Flares → Lens Flares, plus a **Lens Flare Profile** asset

Layers
:   Ghosts, Halo, Streak and Glare. Each one can be turned up, down or off.

Cost
:   Depends slightly on your scene and which Glare mode you pick.
</div>

## How it works

Every frame, HLSLens finds the bright pixels in the image, uses them to draw the flare layers and adds the result to the picture **before tonemapping**.

Since the flare comes from the image itself, anything bright can create it: the sun, car headlights, a neon sign, a lit window, a shiny highlight. If the light moves, the flare moves with it. If the light changes color, so does the flare.

!!! warning
    **Only what is on screen can flare.** A light that is off the edge of the screen or behind the camera makes no flare.

    **Exposure matters too.** The same light can flare or not depending on how bright the image is, so you may need to adjust the thresholds.

Flares are an artistic imitation of a lens, not an exact simulation of one specific real lens. You can shape the look to fit your project.

<figure markdown="span">
  <!-- IMAGE: assets/images/lens-flares/scene.png -->
  ![A night scene with HLSLens lens flares](assets/placeholder.svg)
  <figcaption>A scene with HLSLens lens flares. Nothing was placed by hand. The flares come from the bright signs and windows.</figcaption>
</figure>

## What a flare is made of

A flare is built from four layers. You can mix or disable each of them.

| Layer | What it looks like | Set in |
|---|---|---|
| [Ghosts](#ghosts) | Soft shapes like circles, hexagons or ovals, lined up across the screen. These are copies of the light bouncing around inside the lens. | Lens Flare Profile |
| [Halo](#halo) | A ring around the center of the screen, like the one a wide-angle lens makes. | Lens Flare Profile |
| [Streak](#streak) | A thin horizontal line of light through the light source. The classic look of anamorphic cinema lenses. | Lens Flare Profile |
| [Glare](#glare) | Star-shaped spikes, also called sunburst or starburst. A shape that appears on the light source itself. | Post Process Volume |

## Ghosts

Ghosts are repeated shapes in a flare. They appear on an imaginary line that runs from the light through the center of the screen. When the light moves, the ghosts slide along that line.

Each ghost has a **Scale** that decides where it sits on that line:

| Scale | `−1` | `0` | `0.5` | `1` | `1.5` |
|---|---|---|---|---|---|
| **Position** | Opposite side of the screen | Screen center | Halfway | On the light | Past the light |

Every ghost has its own settings, so each one can have a different size and color. A Lens Flare Profile (a data asset) can hold up to **12 ghosts**. They can be round, oval, sharp-edged or hexagonal, depending on what kind of camera lens you want to replicate.

| Setting | What it does | Default | Range |
|---|---|---|---|
| Color | The color of the ghost. Alpha is its brightness. | White | — |
| Scale | Where the ghost sits on the line. `1` is on the light, `0` is the screen center, negative is the opposite side. | 0.8 | −4 to 4 |
| Size | How big the ghost is, as a fraction of the screen height. `0` gives a small copy of the whole screen. | 0.05 | 0 to 0.5 |
| Softness | How soft the outer edge is. Low is crisp, high is blurry. | 0.35 | 0 to 1 |
| Rim Strength | Brightens the edge of the ghost. `0` gives a flat disc. | 1.0 | 0 to 4 |
| Rim Color | The color of that bright edge. Only visible if Rim Strength is above 0. | White | — |
| Blade Count | Gives the ghost corners, like a camera aperture. `0` is round. More corners look closer to a circle. | 0 | 0 to 16 |
| Aspect | Stretches the ghost. `1` is a circle, higher is wider, lower is taller. | 1.0 | 0.25 to 6 |
| Crescent Offset | Cuts a second disc out of the ghost, leaving a crescent. Negative flips the side. `0` is off. | 0 | −1.5 to 1.5 |
| Align To Axis | Turns the shape to point along the line to the screen center. Only shown for ghosts with blades or a crescent. | Off | — |

??? note "Advanced ghost settings (hidden by default)"

    | Setting | What it does | Default | Range |
    |---|---|---|---|
    | Blade Rotation | Turns the corners of the shape, in degrees. | 0 | 0 to 360 |
    | Blade Roundness | Rounds off the corners. `0` is sharp. | 0 | 0 to 1 |
    | Source Radius Min | The ghost fades out when its light is closer to the screen center than this. `0` is the center, `1` is the corner. | 0 | 0 to 2 |
    | Source Radius Max | The ghost fades out when its light is farther from the center than this. `2` is off. | 2 | 0 to 2 |

!!! tip
    **Source Radius Min** and **Max** let you make ghosts that only show up when the light is near the edge of the screen, or only when it is near the center. It is a nice way to make a flare feel more alive as the camera moves.

## Halo

The halo is a ring around the center of the screen. It is drawn from the same bright pixels as the ghosts. You can make it big or small, soft or sharp, and give it corners like a camera aperture.

| Setting | What it does |
|---|---|
| Halo Intensity | How bright the ring is. |
| Halo Width | How big the ring is. |
| Halo Mask | Fades the ring out near the center of the screen. |
| Halo Compression | Bends the ring, like a fisheye lens would. |
| Halo Aspect Ratio | Stretches the ring wider or taller. |
| Halo Tint | Colors the ring. |
| Halo Softness | How soft the ring is. Low gives a thin, crisp line, high gives a milky glow. |
| Halo Edge Sharpness | How quickly the ring fades at its edges. |
| Halo Ring Smoothness | Smooths out the ring so it looks less like a hard line. |
| Halo Chroma Shift | Splits the colors slightly at the edge, like a real lens does. |
| Halo Blade Count and Strength | Gives the ring corners and spokes, like a camera aperture. |

## Streak

The streak is a thin horizontal line of light running through a bright light, the signature look of anamorphic lenses. It is made of a bright core line, a wider glow around it and some faint extra lines. Each part has its own color, so the streak can shift from a white center to a blue or orange tail.

Not every look uses it. **Canon FD**, **Modern Hex** and **Vintage Veil** have no streak at all, while **Kowa 2x** and **Anamorphic Amber** are built around it. A streak with an Intensity of `0` is skipped completely, so an unused streak costs nothing.

| Setting | What it does |
|---|---|
| Streak Intensity | How bright the streak is. |
| Streak Threshold | How bright a light has to be to get a streak. Raise it if your whole frame turns into a colored wash. The presets use `4`. |
| Streak Length | How long the streak is. |
| Streak Thickness | How thick the line is. |
| Streak Tint | The color of the streak's tail. |
| Streak Core Tint | The color of the bright line in the middle. |
| Streak Band Tint, Intensity and Width | The color, brightness and size of the wider glow around the core line. |
| Streak Secondary Intensity | How visible the faint extra lines are. |

## Glare

Glare is a shape that appears on the light source itself and makes it feel luminous. It is set on the **Post Process Volume**, not in the profile. There are two styles:

| | Three Streak | Directional |
|---|---|---|
| **Look** | A tapered star made of three streaks: one upright and two diagonal. The streaks tilt outward toward the screen edges and get shorter there. | The bright parts of the image are smeared in several directions. Softer, and it follows the shape of the bright area, so a big bright object makes a wide, soft smear. |
| **Feel** | More photographic, less artificial. | More artificial, but with more room for customization. |
| **Cost** | Higher | Much cheaper |

<div class="grid" markdown>
<figure markdown>
  <!-- IMAGE: assets/images/lens-flares/glare-three-streak.png -->
  ![Three Streak glare](assets/placeholder.svg)
  <figcaption>Three Streak glare</figcaption>
</figure>
<figure markdown>
  <!-- IMAGE: assets/images/lens-flares/glare-directional.png -->
  ![Directional Blur glare](assets/placeholder.svg)
  <figcaption>Directional Blur glare</figcaption>
</figure>
</div>

### Shared settings

| Setting | What it does | Default | Range |
|---|---|---|---|
| Glare Mode | Three Streak or Directional. | Three Streak | — |
| Intensity | How bright the glare is. This is the main brightness control and it doesn't change the length. | 0.3 | 0 to 10 |
| Tint | Colors the glare. Alpha `0` hides it. | White | — |

### Three Streak settings

| Setting | What it does | Default | Range |
|---|---|---|---|
| Scale | How long each of the three streaks is (X is the upright one, Y and Z are the diagonals). `0` removes a streak. For example `(1, 0, 0)` leaves only the upright one. | 1, 1, 1 | 0 to 10 |
| Max Size | The longest any streak is allowed to get, no matter how bright the light is. This stops the sun from making a huge glare. | 0.1 | 0.01 to 1 |
| Divider | How bright a light has to be to get a long streak. Higher means only the brightest lights get long ones. Lower means even weak lights get them. | 5 | 0 to 200 |

### Directional settings

| Setting | What it does | Default | Range |
|---|---|---|---|
| Directions | The number of streak arms. `2` gives a cross (+), `3` a 6-point star and `4` an 8-point star. | 3 | 1 to 4 |
| Rotation | Turns the whole star, in degrees. | 0 | 0 to 360 |
| Streak Length (Passes) | How long the streaks are. Each pass makes them 4 times longer. | 3 | 2 to 4 |
| Streak Falloff | How quickly the streak fades from the light to the tip. | 0.87 | 0.80 to 0.99 |
| Vignette Intensity | How strongly the screen edges suppress the glare. This can hide glare popping in and out at the edges. | 0.25 | 0 to 1 |
| Vignette Radius | Where the edge suppression starts. | 0.45 | 0.1 to 0.5 |

### Spectral dispersion

Spectral dispersion colors the streaks based on how far each pixel is from the light. It imitates the rainbow-like color split a real lens creates.

| Setting | What it does | Default | Range |
|---|---|---|---|
| Dispersion Intensity | How strong the color split is. `0` is off. | 0.7 | 0 to 1 |
| Spectral Gradient | An optional 1D gradient texture. The left edge is the color at the light, the right edge is the color at the tip. | None | Texture |
| Dispersion Bias | Moves the colors along the streak. Positive pushes them toward the tips and keeps more of the streak white. | 0.2 | −1 to 1 |
| Dispersion Contrast | Higher gives a sharper switch between the colors. Lower blends them smoothly. | 2.0 | 0.5 to 6 |

!!! performance "Performance"
    **Directional** is much cheaper than Three Streak, and it has more settings to play with. If performance is important, use it. With some tweaking it can look quite close to the Three Streak glare.

## Lens Flare Profiles and presets

Ghosts, Halo and Streak are saved in a **Lens Flare Profile**, a `UDataAsset` you create in the Content Browser. One profile is one complete lens: its ghosts, its halo and its streak. Glare and bloom are set on the volume.

The Post Process Volume references a profile and has three intensity sliders (Ghost, Halo and Streak) to adjust each layer.

This means a flare look is just data that you can save and reuse across levels. Five presets come with the plugin. Open a profile and use the preset buttons to reset it to one of them, then change any settings you want.

| Preset | Look |
|---|---|
| Canon FD | Many soft, colored ghosts. Small bright spots near the light, bigger see-through ones further out, and a halo. No streak. |
| Kowa 2x | A blue anamorphic streak, wide blue oval ghosts and a wide blue halo. |
| Anamorphic Amber | A warm orange streak with amber and teal ovals. |
| Modern Hex | Crisp, hexagon-shaped ghosts in green, magenta and blue, and a thin, faceted ring. No streak. |
| Vintage Veil | Milky, warm and low in contrast. A big soft halo and a few faint ghosts. |

<div class="grid" markdown>
<figure markdown>
  <!-- IMAGE: assets/images/lens-flares/preset-canon-fd.png -->
  ![Canon FD preset](assets/placeholder.svg)
  <figcaption>Canon FD</figcaption>
</figure>
<figure markdown>
  <!-- IMAGE: assets/images/lens-flares/preset-kowa-2x.png -->
  ![Kowa 2x preset](assets/placeholder.svg)
  <figcaption>Kowa 2x</figcaption>
</figure>
<figure markdown>
  <!-- IMAGE: assets/images/lens-flares/preset-anamorphic-amber.png -->
  ![Anamorphic Amber preset](assets/placeholder.svg)
  <figcaption>Anamorphic Amber</figcaption>
</figure>
<figure markdown>
  <!-- IMAGE: assets/images/lens-flares/preset-modern-hex.png -->
  ![Modern Hex preset](assets/placeholder.svg)
  <figcaption>Modern Hex</figcaption>
</figure>
<figure markdown>
  <!-- IMAGE: assets/images/lens-flares/preset-vintage-veil.png -->
  ![Vintage Veil preset](assets/placeholder.svg)
  <figcaption>Vintage Veil</figcaption>
</figure>
</div>

### Blending between profiles

When post-process volumes overlap, HLSLens blends their profiles using the volume weights. Colors and numbers are blended smoothly. Values that can't blend, like the number of blades on a ghost, switch over once the blend passes halfway. Ghosts are blended slot by slot, so a ghost that only exists in one profile fades in or out.

For example, you can use this to move smoothly from a sunny outdoor area with a warm vintage lens into a dark corridor with a cold anamorphic one.

## Volume settings

| Setting | What it does | Default | Range |
|---|---|---|---|
| Flares Master Intensity | Brightness of the whole flare effect. | 1.0 | 0 to 10 |
| Tint | Colors the whole flare. | White | — |
| Master Gradient | A gradient texture that masks or colors the flare based on its distance from the center of the screen. | Default | Texture |
| Ghost Intensity | Multiplies the ghost intensity of the profile. | 1.0 | 0 to 4 |
| Halo Intensity | Multiplies the halo intensity of the profile. | 1.0 | 0 to 4 |
| Streak Intensity | Multiplies the streak intensity of the profile. | 1.0 | 0 to 4 |
| Lens Flare Threshold Level | How bright a pixel must be to make a flare. High values mean only the brightest lights flare. | 1.0 | 0 and up |
| Lens Flare Threshold Knee | How soft the cut-off is. At `0` flares switch on sharply. | 0.5 | 0 and up |

!!! tip
    Want a different color mood? Change the **Tint**, or make your own gradient and use it instead of the default **Master Gradient**.

## Common questions

??? question "Do I need to add flares or do any setup for each of my lights?"
    No. Flares are procedural. The shader adds them automatically where they need to be.

??? question "Are the flares just images?"
    No. Every ghost, ring and streak is drawn by the shader in HLSL from your scene.

??? question "Why is there no flare?"
    - Make sure the **Lens Flare Threshold Level** isn't too high.
    - Check that the **Ghost**, **Halo** and **Streak Intensity** sliders are above 0.
    - Exposure changes how bright things are, so you may need to increase it.
    - Make sure the Advanced Post Process Volume is set to **Unbound**, or scaled so that your camera is inside it.

??? question "My whole screen is covered in color."
    Raise the **Streak Threshold** or the **Lens Flare Threshold Level**, or lower the intensities.

??? question "How is this different from the engine's lens flare?"
    The engine's lens flare gives you a fixed set of ghosts. HLSLens lets you design every ghost, and it adds the halo, streak and glare layers.
