# Reporting issues to WineHQ

**Warning**: This guide is only recommended for advanced users. If facing issues, please follow [Troubleshooting](./index.md) instructions first.

Vinegar can be configured to help you diagnose if a bug/issue is caused by Wine and make a report to WineHQ without violating their reporting guidelines.

First of all, create a new toml configuration file in an appropriate location, with the following content:
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
Read over every option carefully and follow the instructions in the comments.

**Critical**: This configuration file depends heavily on your Vinegar version! <u>Do **NOT** reuse it</u>, especially after updating Vinegar. Recheck this guide to ensure you have the latest version of the configuration.

Once the file is ready, set the `WINEPREFIX` env var to a temporary location, then run Vinegar with the `-config (filepath)` flag to use the cfg you just created. 

The command should be similar to this if all steps were followed correctly: `WINEPREFIX=/tmp/report vinegar -config /home/jrelvas/Documents/winehq-report.toml player`.

Caveat: Your desktop entries will obviously not be affected by this, preventing you from logging into studio or executing actions from roblox.com properly. You will have to edit them to reflect the changes above.

**Warning**: Keep in mind that any issues you face while following these steps are unsupported and should not be reported to us.