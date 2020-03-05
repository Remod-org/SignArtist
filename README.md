# SignArtist (Remod version)

[Download](https://code.remod.org/SignArtist.cs)

Note: The code that handles the resizing requires gdiplus.dll. This should be present on Windows machines. But, on Linux, you will most likely have to install the package libgdiplus. Because this library depends on mono you will also have to add the mono repository to your system. Please refer to the FAQ to see how to do this.

This plugin allows players with the appropriate permission to use images from the internet to display on signs.
Configuration
The settings and options for this plugin can be configured in the SignArtist.json file under the oxide/config directory. The use of a JSON editor or validation site such as jsonlint.com is recommended to avoid formatting issues and syntax errors.

```json
{
  "Time in seconds between download requests (0 to disable)": 0,
  "Maximum concurrent downloads": 5,
  "Maximum distance from the sign": 3,
  "Maximum filesize in MB": 1.0,
  "Enforce JPG file format": false,
  "JPG image quality": 0,
  "Enable logging file": false,
  "Enable logging console": false
}
```

A few notes about some configuration values:

    Maximum concurrent downloads is also used for a separate restore queue, so the plugin will never try to restore more signs at the same time than the value entered here.
    JPG image quality is a numeric value between 0 and 100 (inclusive) that defines the jpeg image quality when the image is saved to storage.

# Permissions
This plugin uses Oxide's permission system. To assign a permission, use oxide.grant <user or group> <name or steam id> <permission>. To remove a permission, use oxide.revoke <user or group> <name or steam id> <permission>.

    signartist.urlAllows the player to use the /sil command
    signartist.textAllows the player to use the /silt command
    signartist.restoreAllows the player to use the /silrestore command
    signartist.ignoreownerAllows the player to use the /sil and /silt commands when he does not have building permissions
    signartist.ignorecdAllows the player to use the /sil and /silt commands without trigger a cooldown.
    signartist.rawAllows the player to specify the raw argument to ignore the jpeg enforcement when it is enabled in the config
    signartist.restoreallAllows the player to specify the all argument for /silrestore to restore all signs at once.

# Commands
## Chat Commands

    /sil <url> [raw]Download the image from the url to the server and display it on the sign you are currently looking at. Specifying the `raw` argument allows you to ignore jpeg enforcement if that is enabled in the config file.
    /silt <message> [<fontsize: number>] [<color: hex value>] [<bgcolor: hex value>] [raw]Downloads a generated image with the given text and optional fontsize, color, bgcolor to be displayed on the sign you are currently looking at. Specifying the raw argument allows you to ignore jpeg enforcement if that is enabled in the configuration file.
    /silrestore [all] [raw]Restores an image on the sign that was broken during the last Rust update. Specifying the all argument will restore all signs on the server. Specifying the raw argument allows you to ignore jpeg enforcement if that is enabled in the configuration file.

(Keep in mind, if the sign is from a copy/pasted building you will have to save it again to correctly save the files for copy/paste for future use, unless you want to restore after every paste ;) )
## Console Commands

These console commands do the exact same thing as the chat commands and can only be executed from the ingame console. They were added to allow input (long urls and such) that can't be send through chat.

    sil <url> [raw]
    silt <message> [<fontsize: number>] [<color: hex value>] [<bgcolor: hex value>] [raw]

# Examples

Load from URL/sil https://assets.umod.org/images/umod-gray-nomargin.png

Load from local file/sil file:///C:/Windows/test.png/sil file:///c:\img\test.png (might work better). On Windows, be sure to work in a directory that's not restricted for some reason, e.g. C:\Windows.

# For Developers

```csharp
    private void signText(BasePlayer player, Signage sign, string message, int fontsize=30, string color="FFFFFF", string bgcolor="000000")
```

```csharp
    private void Silt(Signage sign, string message, int fontsize=30, string color="FFFFFF", string bgcolor="000000")
```

```csharp
    private void signImage(BasePlayer player, Signage sign, string url, bool raw = false)
```

```csharp
    private void Sil(Signage sign, string url, bool raw = false)
```

```csharp
    private object GetSignLookedAt(BasePlayer player)
```

```csharp
    private bool IsSignHorizontal(Signage sign)
```

# Credits

    Nogrod, the original author of this plugin
  
