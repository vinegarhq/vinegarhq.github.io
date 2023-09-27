# Reporting issues to WineHQ

Whenever you run into an issue with Vinegar, the culprit could be one (or more) of its many components and libraries (Vinegar itself, Wine, DXVK, etc.), but more often than not, said culprit is Wine.
Vinegar can be configured to help you diagnose if a bug/issue is caused by Wine and make a report to WineHQ without violating their reporting guidelines.

**Warning**: This guide is not recommended unless you're an advanced user. Please follow [Troubleshooting](./index.md)'s instructions instead.

First of all, create a new toml configuration file somewhere accessible to you, with the following content:
```toml
# Written for Vinegar v1.4.4.

# WARNING: This should be left empty if your system has WineHQ packages installed (https://wiki.winehq.org/Download).
# Otherwise, either install WineHQ packages or set wineroot to a staging/development wine's path.
# TL;DR: Ensure Vinegar uses a staging/development wine, otherwise your report is INVALID.
wineroot = "" 

# Symbols definition:
# (X)   = DO NOT EDIT: This option should never be changed. (will invalidate all reports) 
# (?)   = This option may be edited. In case of doubt, do not change.
# (...) = User defined options can be added here (not recommended, may invalidate your report)

dxvk_version = ""           # (X)
multiple_instances = false  # (X)
sanitize_env = false        # (X)

[env]
WINEDEBUG = ""              # (?): Use this to increase Wine log verbosity.
# (...)
DXVK_LOG_PATH = ""          # (X)
WINEESYNC = ""              # (X)
WINEFSYNC = ""              # (X)
WINEDLLOVERRIDES = ""       # (X)

[player]
channel = ""                # (?): Use this to debug a specific Roblox version.           
forced_version = ""         # (?): Use this to debug a specific Roblox version.       
renderer = "D3D11"          # (?): Use this to debug a specific renderer. (D3D11 will use Wine's built-in D3D opengl conversion.)
dxvk = false                # (X)
auto_kill_prefix = false    # (X)
launcher = ""               # (X)

[studio]
channel = ""                # (?): Use this to debug a specific Roblox version.           
forced_version = ""         # (?): Use this to debug a specific Roblox version.       
renderer = "D3D11"          # (?): Use this to debug a specific renderer. (D3D11 will use Wine's built-in D3D opengl conversion.)
dxvk = false                # (X)
auto_kill_prefix = false    # (X)
launcher = ""               # (X)

[player.fflags]
DFIntTaskSchedulerTargetFps = 60 # (X)
```
Read over every option carefully. Some can (and should) be edited! Follow the instructions in the comments.

**Critical**: This configuration file depends heavily on your Vinegar version! <u>Do **NOT** reuse it</u>, especially after updating Vinegar. Recheck this guide to ensure you have the latest version of the configuration.

Once you have created the file, you have to tell Vinegar to use it instead of your default/normal configuration. This can be done using the `-config (filepath)` flag!
Lastly, you must specify a wine prefix for Vinegar to use, to ensure any existing data does not interfere with your report. This can be done by setting the env variable `WINEPREFIX` to your desired location. This can be anywhere, even `/tmp`. as long as Vinegar has access to it.

Assuming that you placed your configuration file in your Documents folder and that it's named `winehq-report.toml`, you should run the following command to test Roblox player (for example): `WINEPREFIX=/tmp/report vinegar -config /home/jrelvas/Documents/winehq-report.toml player`.

If you followed these instructions correctly, Vinegar...
- Will use a Staging/Devel WineHQ Build of Wine
- Will use a clean, unmodified wineprefix
- Will provide a bit of extra debug logs by default
- Will not use DXVK or any other non-wine DLLs or libraries
- Will not use any special workarounds or settings
- Will not use or touch your existing configuration
- Will not have any special functionality not provided by Wine
- Will essentially just act as a Roblox Player/Roblox Studio installer and bootstrapper, with no other functionality or features

Caveat: Your .desktop files will obviously not be affected by this. This means you won't be able to log into studio or open links/games from roblox.com. The workaround is to manually edit the desktop file so it uses the right `-config` flag and `WINEPREFIX`. They can be found at `usr/share/applications`. 

Note that env variables in .desktop Exec commands must be declared with the `env` command. For example: Do `env WINEPREFIX = /tmp/report vinegar -config /home/jrelvas/Documents/winehq-report.toml player` instead of `WINEPREFIX=/tmp/report vinegar -config /home/jrelvas/Documents/winehq-report.toml player`

**Warning**: After following these steps, ensure your report follows [WineHQ.org's bug report guidelines](https://wiki.winehq.org/Bugs).

**Warning**: Keep in mind that any issues you face while following these steps are unsupported and should not be reported to us.