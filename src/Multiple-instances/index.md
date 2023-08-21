# Multiple instances

To run multiple instances of the Roblox Player (Studio untested), there are two methods:

* Multiple Wineprefixes; While this solution works, it requires Vinegar to manage both wineprefixes for Studio or Player (or multiple Player wineprefixes for each instance), with no control over which one is preferred and launched, this can be a problem for DXVK. Additionally the Wineprefix size is often more than 700MB.
* Roblox Mutex override; Roblox when running will create a Mutex file to indicate that it is running, other instances of Player will check for if this Mutex belongs to the Player and refuses to launch.

## Roblox Mutex override

In Vinegar's repository, there is a program called `robloxmutexer` which requires `winegcc` or MinGW installed to compile. This is due to the fact that UNIX like operating systems (Linux included) do not have named Mutexes, and also that WINE's Mutexes may nor may not be shared with the host operating system. For this, this program must run under the Wineprefix in which Player is running in.

You can compile `robloxmutexer` in the source directory of Vinegar:
```sh
make robloxmutexer
# make WCC=winegcc robloxmutexer
```
Since this is a Windows executable, it is not recommended to install it.

To run the program:
```
vinegar exec ./robloxmutexer.exe
```
This program must be launched *before* Player is running, after it says `roblox mutex locked`, you may run Player, and multiple instances of it.

Please note that if you try to compile this program using Flatpak MinGW Runtime and run it, you cannot run multiple Wineprefixes at once, you must run this program in the foreground as the same sandbox session as the other Roblox instances.
