# Bloom

<p class="lead">Bloom is the soft glow around bright objects.</p>

In real life, camera lenses and our eyes scatter a bit of light from anything bright, so a street lamp doesn't have a sharp edge, it glows. Bloom recreates that, and it is a big part of why a scene feels bright instead of flat.

HLSLens replaces Unreal's built-in bloom. It works on the final image, so you don't set anything up on your lights. Anything bright can glow: lights, emissive materials, the sky or something shiny.

<div class="glance" markdown>
Where to find it
:   Post Process Volume → Bloom & Lens Flares → Bloom

Cost
:   Standard is cheap. Cinematic does twice the work. A higher Blur Pass Amount costs more too.
</div>

## How bloom works

The bloom is built in four steps. You don't have to touch any of them, but knowing how it works makes the settings easier to understand.

<div class="steps" markdown>
<div markdown>
<span class="n">1 · Isolate</span>
Pick out the bright parts of the image. This step is optional.
</div>
<div markdown>
<span class="n">2 · Shrink</span>
Make smaller, blurrier copies of the image. Each one is about twice as blurry as the last.
</div>
<div markdown>
<span class="n">3 · Weight</span>
Decide how much each copy counts. The Falloff setting controls this.
</div>
<div markdown>
<span class="n">4 · Merge</span>
Stack the copies back together into one smooth glow.
</div>
</div>

!!! note
    A bright light keeps all of its energy through these steps, so even a small lamp gets a big, soft halo without cranking up Intensity.

    The engine's default bloom uses a fixed number of blur steps, and in some scenes you can see rings in the glow where those steps meet. HLSLens blends everything into one smooth curve, so the glow fades without these rings and lines.

## Standard and Cinematic quality

There are two quality modes. The look stays about the same in both. Cinematic is smoother and unlocks three extra settings.

| | Standard | Cinematic |
|---|---|---|
| **Blur steps** | Normal amount | Twice as many, so it's smoother |
| **Smoothness** | Smooth | Smoother, with no faint steps in the glow |
| **Extra settings** | None | Haze Ignores Threshold, Halo Brightness Boost, Spectral Spread |
| **Cost** | Low | About twice the work of Standard |

!!! performance "Performance"
    Start with **Standard**. Switch to **Cinematic** only if you can see a meaningful difference in your scene. The difference between the two isn't massive.

## Threshold: choosing what blooms

The threshold decides how bright a pixel has to be before it blooms. Anything darker than the **Threshold Level** is ignored. The **Knee** softens the cut-off.

| Setting | What it does | Default |
|---|---|---|
| Threshold Mode | Chooses which effects use a threshold. **Shared** is the one to pick when Bloom and Lens Flares are both on: both use the same values, and it runs faster than two separate thresholds. | None |
| Threshold Level | How bright a pixel has to be before it blooms. Lower values make more of the image glow. Comes in a Shared, a Bloom and a Lens Flares version. | 1.0 |
| Threshold Knee | How soft the cut-off is. Also comes in a Shared, a Bloom and a Lens Flares version. | 0.5 |

!!! tip
    For a fully realistic look, turn the threshold off. In the real world every bright surface blooms a little, with no hard cut-off. Using a threshold is still a great way to keep the scene from blooming too much and getting a dreamy look.

## Shaping the glow

The shape of the glow comes from **Falloff** and three intensity sliders. Take a street lamp as an example:

- The **core** is the sharp, bright part right around the bulb.
- The **body** is the medium glow, where most of the bloom is.
- The **haze** is the wide, faint glow further around it.

| Setting | What it does | Default | Range |
|---|---|---|---|
| Falloff | How fast the glow fades away from a light. Lower values give more wide haze, higher values keep the glow tight. It moves light between tight and wide glow without changing the overall brightness. | 2.4 | 1.5 to 4.0 |
| Core Intensity | Brightness of the sharp part right around a light. | 1.0 | 0 to 4 |
| Body Intensity | Brightness of the medium glow. This is where most of the visible bloom is. | 1.0 | 0 to 4 |
| Haze Intensity | Brightness of the widest, faintest glow. | 1.0 | 0 to 4 |
| Haze Size | How far the haze reaches. `0` is only the tight glow, `1` is the full reach. | 1.0 | 0 to 1 |

Use these Falloff values as a starting point:

| Falloff | Look |
|---|---|
| About 2.0 | Hazy, dreamy, foggy lights. |
| 2.4 to 2.8 | Default. |
| Above 3.5 | A tight glow. The haze almost disappears. |

!!! tip
    Falloff and the three intensities are independent of the overall **Intensity**. You can change the character of the glow, for example less haze and a stronger core, without rebalancing its brightness afterwards.

## Cinematic-only settings

These settings only work when **Bloom Quality** is set to **Cinematic**.

| Setting | What it does | Default | Range |
|---|---|---|---|
| Haze Ignores Threshold | Normally the haze only comes from pixels above the threshold. Turn this up and the widest haze is made from the whole image instead, like the soft veil of light on a real lens. It also stops the glow from suddenly popping when something crosses the threshold. Does nothing if the threshold is off, and costs a bit more. | 0 | 0 to 1 |
| Halo Brightness Boost | Gives much brighter areas a bigger halo, so the sun gets a bigger halo than a small lamp. An artistic effect, not a realistic one. `0` is off. | 0 | 0 to 4 |
| Spectral Spread | Makes the red part of the glow reach a bit further than the blue part, like on a real lens. You get a subtle warm edge on the outer glow without changing the overall color of your scene. `0` is off. | 0.25 | 0 to 1 |

## Strength, color and reach

| Setting | What it does | Default | Range |
|---|---|---|---|
| Intensity | How strong the bloom is overall. | 0.4 | 0 to 10 |
| Tint | Colors the bloom. Darker values make it weaker, and black hides it. | White | — |
| Blur Pass Amount | How far the bloom can spread across the screen. Higher means a wider glow and a higher GPU cost. Lower keeps the glow close to the light. | — | 1 to 10 |
| Dirt Mask | A texture that looks like dust and smudges on a camera lens. It shows up where the bloom is bright. | None | Texture |
| Dirt Mask Tint | Colors the dirt. | White | — |
| Dirt Mask Intensity | How visible the dirt is. `0` hides it. | 1.0 | 0 to 10 |

## Looks you can create

A few ideas to try. Tune the settings to fit your scene, but these give you a direction.

| Look | Where to start |
|---|---|
| Soft, filmic night scene | Lower Falloff (around 2.0 to 2.4) and plenty of Haze Intensity. Big, soft halos around street lights. |
| Car headlights | Higher Falloff and Core Intensity. Tight, bright cores. |
| Overexposed sunlight | Cinematic quality with Halo Brightness Boost raised, so very bright areas get a big glow. |
| Dreamy or horror | Falloff near 2.0, lots of Haze Intensity and full Haze Size. In Cinematic, try Haze Ignores Threshold too. |
| Clean and natural | Leave everything at the defaults and adjust Intensity. |

## Compared with the engine's bloom

These images show the same bright light with the engine bloom and the HLSLens bloom. Zoom in to see the difference. Both blooms are customizable, so the exact look depends on the settings.

The engine bloom uses its default settings with only **Bloom Intensity** and **Bloom Gaussian Intensity** increased. For HLSLens, only **Bloom Intensity** was increased.

<figure markdown="span">
  <!-- IMAGE: assets/images/bloom/comparison-linear.png -->
  ![Engine bloom compared with HLSLens bloom](assets/placeholder.svg)
  <figcaption><strong>Figure 1.</strong> One bright light with the engine bloom (top) and the HLSLens bloom (bottom). The middle shows brightness across the light. On the right both are overlaid: red is the engine, green is HLSLens, yellow is where they match.</figcaption>
</figure>

<figure markdown="span">
  <!-- IMAGE: assets/images/bloom/comparison-log.png -->
  ![Bloom comparison on a log scale](assets/placeholder.svg)
  <figcaption><strong>Figure 2.</strong> The same comparison on a log scale, which makes the faint edge of the glow easier to see. Flat steps in the curve are what show up as rings in the glow.</figcaption>
</figure>

## Common questions

??? question "Do I need to add anything to my lights?"
    No. You don't need to add any textures. Anything bright enough will glow.

??? question "Why is nothing glowing?"
    - Check that **Intensity** is above 0 and **Tint** isn't black.
    - Check the threshold. If **Threshold Level** is too high, the bloom won't be visible.
    - Make sure your exposure is high enough.

??? question "The screen is washed out in white."
    Lower **Intensity**, raise the **Threshold Level**, make the bloom **Tint** darker, or raise **Falloff** to keep the glow tighter.

??? question "Does Falloff make the scene brighter or darker?"
    Not really. Use **Intensity** for brightness.

??? question "How is bloom different from lens flares and halation?"
    Bloom is the soft glow around bright areas. [Lens flares](lens-flares.md) are the shapes a camera lens adds. [Halation](halation.md) is a separate effect that imitates film. They work well together.
