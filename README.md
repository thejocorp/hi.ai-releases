# hi.ai

### From `"Hello, World!"` to `hi.ai`

*Built for AI professionals and newcomers ready to use AI like a pro.*

**Go from Prompt Engineering to Harness Engineering, all within a single app.**

## Install

Paste one line and press Enter. It downloads the newest release from the [releases page](https://github.com/thejocorp/hi.ai-releases/releases) and installs it. Start hi.ai and the setup wizard takes it from there.

**Linux and macOS.** Open a terminal (on a Mac: the Terminal app, in Applications, Utilities) and paste:

```sh
curl -fsSL https://github.com/thejocorp/hi.ai-releases/releases/latest/download/install.sh | sh
```

On Debian, Ubuntu, Kali and their relatives it installs the deb package and asks for your password once. Other Linux desktops get the AppImage in `~/.local/bin` and a menu entry. A Linux without a desktop gets the server alone, which you open in a browser. On a Mac it needs Apple silicon (M1 or newer) and puts hi.ai in Applications.

**Windows.** Open PowerShell from the Start menu and paste:

```powershell
irm https://github.com/thejocorp/hi.ai-releases/releases/latest/download/install.ps1 | iex
```

It installs hi.ai for your user, so it needs no admin rights, and adds it to the Start menu.

**Updates.** When a new release is out, hi.ai asks you. Update now downloads it, checks its signature, installs it and opens hi.ai again; Later asks again at the next start. The server alone, without the app window, does not update itself: run the install line again.

I develop and use hi.ai on Linux; the Windows and macOS builds are new, so tell me in an [issue](https://github.com/thejocorp/hi.ai-releases/issues) what breaks. Every release is installed with the lines above on Linux, Windows and macOS before it becomes the newest. The files are not signed by Apple or Microsoft, so a file you download in a browser gets a warning (on Windows: More info, then Run anyway; on a Mac: System Settings, Privacy & Security, Open Anyway). The install lines download without a browser and get none.

