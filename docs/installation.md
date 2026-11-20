# Installation

Getting HLSLens into a project takes three steps.

1.  **Create or open an Unreal Engine 5 project.**

    The examples in this documentation use the **First Person** template in Unreal Engine 5.8. The Third Person template works the same way, though some names may differ.

2.  **Install the plugin.**

    Install HLSLens from Fab (the Epic Marketplace), or copy the plugin into your project's `Plugins` folder:

    ```text
    YourProjectName/
    └── Plugins/
        └── HLSLens/
    ```

    If the `Plugins` folder does not exist, create it.

3.  **Enable the plugin.**

    In the editor, go to **Edit → Plugins**, search for **HLSLens** and enable it. Restart the editor if prompted.

<figure markdown="span">
  <!-- IMAGE: replace with your screenshot, e.g. assets/images/installation/plugins-folder.png -->
  ![The project folder with the Plugins folder highlighted](assets/placeholder.svg)
  <figcaption>Create the highlighted <code>Plugins</code> folder if you do not have it, then add the <code>HLSLens</code> folder into it.</figcaption>
</figure>

!!! tip "Next step"
    Place an **Advanced Post Process Volume** in your level. All HLSLens effects read their settings from it. Then continue with [Lens flares](lens-flares.md), [Bloom](bloom.md) or [Halation](halation.md).
