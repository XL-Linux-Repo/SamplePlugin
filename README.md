# SamplePlugin

Simple example plugin for Dalamud, but adjusted slightly to serve as a jumpstart for building from Linux.

This is not designed to be the simplest possible example, but it is also not designed to cover everything you might want to do. For more detailed questions, go ask in [the XL Discord](https://discord.gg/3NMcUV5).

## Main Points

* Simple functional plugin
  * Slash command
  * Main UI
  * Settings UI
  * Image loading
  * Plugin json
* Simple, slightly-improved plugin configuration handling
* Project organization
  * Copies all necessary plugin files to the output directory
    * Does not copy dependencies that are provided by dalamud
    * Output directory can be zipped directly and have exactly what is required
  * Hides data files from visual studio to reduce clutter
    * Also allows having data files in different paths than VS would usually allow if done in the IDE directly


The intention is less that any of this is used directly in other projects, and more to show how similar things can be done.

## To Use
### Building

1. Clone the repository
2. Open up `SamplePlugin.sln` in your C# editor of choice (likely [Visual Studio 2022](https://visualstudio.microsoft.com) or [JetBrains Rider](https://www.jetbrains.com/rider/)).
3. Create a symbolic link to the XIV launch folder, or adjust your OutputPath and DalamudLibPath accordingly.
    * Symbolic link would be, while in the root of your project folder, `ln -s <XIVLauncherFolderPath> ./XIVLauncher`
4. Build the solution. By default, this should build to `./XIVLauncher/devPlugins/SamplePlugin` (assuming your path is set correctly).
    * This will also build to `SamplePlugin/obj/x64/Debug/SamplePlugin.dll` (or `Release` if appropriate.)

### Activating in-game

1. Launch the game and use `/xlsettings` in chat or `xlsettings` in the Dalamud Console to open up the Dalamud settings.
    * In here, go to `Experimental`, and add the full path to the `SamplePlugin.dll` to the list of Dev Plugin Locations.
    * NOTE: This path will be Windows file path format, with `drive_c` acting as your `C:\`.
        * This means your path should be `C:\users` rather than `drive_c\users`.
2. Next, use `/xlplugins` (chat) or `xlplugins` (console) to open up the Plugin Installer.
    * In here, go to `Dev Tools > Installed Dev Plugins`, and the `SamplePlugin` should be visible. Enable it.
3. You should now be able to use `/pmycommand` (chat) or `pmycommand` (console)!

Note that you only need to add it to the Dev Plugin Locations once (Step 1); it is preserved afterwards. You can disable, enable, or load your plugin on startup through the Plugin Installer.

### Reconfiguring for your own uses

Basically, just replace all references to `SamplePlugin` in all of the files and filenames with your desired name. You'll figure it out 😁

Dalamud will load the JSON file (by default, `SamplePlugin/SamplePlugin.json`) next to your DLL and use it for metadata, including the description for your plugin in the Plugin Installer. Make sure to update this with information relevant to _your_ plugin!