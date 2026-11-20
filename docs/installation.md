# Installation

=== "Fab / Marketplace"

    1. Open the Epic Games Launcher and find the plugin in your **Library**.
    2. Click **Install to Engine** and pick your engine version.
    3. Open your project, go to **Edit → Plugins** and enable **My Plugin**.
    4. Restart the editor.

=== "Project plugin"

    1. Copy the `MyPlugin` folder into your project's `Plugins/` directory.
    2. Right-click the `.uproject` file and choose **Generate Visual Studio project files**.
    3. Build the project and enable the plugin in **Edit → Plugins**.

!!! warning "C++ projects"
    Rebuild the project after switching engine versions.
