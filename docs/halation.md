# Halation

<p class="lead">Halation is the red-orange glow you see around very bright lights on film.</p>

It comes from the film itself. Light passes through the film, bounces off the back of it and exposes the film a second time, so a soft glow appears around the brightest spots. HLSLens recreates that look.

The glow is deep red around lights that are only just bright enough and turns orange around the really bright ones. It doesn't simply copy the color of the light: you choose the glow colors yourself.

Halation works really well with [bloom](bloom.md). It is also great for creating dreamy scenes.

<div class="glance" markdown>
Where to find it
:   The Post Process Volume's Details panel. Every setting has a tooltip in the editor.

Cost
:   Almost free. It reuses the bloom texture.

Works with
:   Bloom. Halation is built from it.
</div>

## Halation or bloom?

It is easy to mistake halation for an orange bloom, but they are different effects. Bloom is light scattering in a lens or your eye. Halation is light bouncing around inside film. You can use both together.

| | Bloom | Halation |
|---|---|---|
| **Imitates** | A lens or an eye | Film |
| **Color** | Takes the color of the light | Mostly its own red-orange color |
| **Which lights** | Everything bright. A threshold is optional. | Only lights above its own threshold |
| **Brightness** | One color at any brightness | Shifts from red to orange as lights get hotter |
| **Bright backgrounds** | Doesn't care what is behind it | Fades out over bright backgrounds |

Halation also looks at what is around the light. The light itself hides the glow, so you only see it on the darker pixels next to it. That is why it looks like a halo around a light and not a tint on top of it.

!!! tip
    Halation works best in dark or night scenes with strong lights against dark surroundings: street lamps, neon, headlights, fire and windows. Keep it subtle. It is not very useful in bright daytime scenes, where it fades out anyway.

!!! note
    Halation is built from the bloom texture, so its size and shape follow your bloom settings. It also checks the blurred bloom, not the raw pixels. Tiny lights get diluted and may need a lower threshold, and exposure changes which lights qualify.

## Example

<div class="grid" markdown>
<figure markdown>
  <!-- IMAGE: assets/images/halation/with.png -->
  ![Scene with halation](assets/placeholder.svg)
  <figcaption>With halation</figcaption>
</figure>
<figure markdown>
  <!-- IMAGE: assets/images/halation/without.png -->
  ![Scene without halation](assets/placeholder.svg)
  <figcaption>Without halation</figcaption>
</figure>
</div>
