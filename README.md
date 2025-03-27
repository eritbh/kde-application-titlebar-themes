# kde-application-titlebar-themes

A set of application-specific KDE Plasma titlebar themes that match the titlebar's colors to the rest of the application's UI without giving up the full native titlebar.

![](.github/preview.png)

## Supported applications

- [1Password](/1password)
- [Apple Music](/apple-music)
- [Discord](/discord)
- [GIMP](/gimp)
- [Konsole](/konsole)
- [Microsoft Teams](/teams)
- [Obsidian](/obsidian)
- [Slack](/slack)
- [Spotify](/spotify)
- [Vivado](/vivado)
- [Visual Studio Code](/vscode)
- [XIVLauncher](/xivlauncher)

Want a theme for another application? [Request it!](https://github.com/eritbh/kde-application-titlebar-themes/issues/new?template=theme-request.md)

## Installing and Using

Titlebar themes are provided as `.colors` files which can be downloaded and placed in `~/.local/share/color-schemes`.

Alternatively, this repository contains a `.stowrc` for use with [`stow`](https://www.gnu.org/software/stow/) (`apt install stow`, etc). Clone this repository somewhere persistent, then use `stow` from the repo root to automatically link the desired themes into `~/.local/share/color-schemes`. For example, you can install all the color schemes for Apple Music, Discord, and Slack all at once with `stow apple-music discord slack`. See [the `stow` manual](https://www.gnu.org/software/stow/manual/stow.html) for more information about this installation method.

Once you've installed the themes you want, window rules can then be used to apply titlebar themes to specific applications.

### Configuring via GUI

There are two ways to create a window rule via a GUI:

- Right-click the native titlebar, and go to More Actions > Configure Special Application Settings. This will open the window rule editor for the current application, with the window class pre-filled.

- Open System Settings > Window Management > Window Rules. This will show you all your window rules and allow you to create new rules. You'll need to create a rule that matches the window class of the desired application; see [Finding an application's window class](#finding-an-applications-window-class). This method is useful for applications which don't present a native titlebar, since you can also [use window rules to force the native titlebar](#forcing-applications-to-use-a-native-titlebar).

Once you have a rule for the application, add the property "Titlebar color scheme", set the first dropdown to "Force", and select the color scheme you want in the second dropdown.

![](.github/kde%20window%20properties.png)

### Configuring directly in `kwinrulesrc`

Window rules are stored in `~/.config/kwinrulesrc` and you can edit this file manually if you want. You can find an example [in my (old, potentially outdate) personal dotfiles repo](https://github.com/eritbh/dotfiles/blob/main/kde/.config/kwinrulesrc).

If you store your dotfiles in version control, this is a useful file to track alongside your `~/.local/share/color-schemes` folder to sync your application-specific titlebar theme configurations across computers.

### Finding an application's window class

Under Xorg, you can use the `xprop` command to find the window class of any window. Run `xprop WM_CLASS` in your terminal, then click on the window you want to identify.

Wayland doesn't use `xprop`, so the way you get information about windows will vary from system to system. [This reddit post](https://www.reddit.com/r/kde/comments/1c447nc/anything_like_xprop_in_wayland_to_get_window/) lists a handful of strategies you can use, the most straightforward being to open the KWin debug console or using the command `qdbus6 org.kde.KWin /KWin queryWindowInfo` and looking for the `resourceClass` of the target window.

### Forcing applications to use a native titlebar

Many applications which draw their own custom titlebars on other platforms give Linux users an option to present the native titlebar instead. If not, KDE window rules can be used to force the native titlebar to show up anyway. To do this, add the "No titlebar and frame" property to the application's window rule, set the dropdown to "Force" and select the "No" option.

![](.github/kde%20force%20window%20frame%20property.png)

Note that if the application presents its own non-native menu bar, KDE does not have a way to hide that. You will have to check the specific application for an option to hide the baked-in titlebar, or use other tweaks (e.g. some Electron-based applications allow you to apply CSS to the UI, which can usually be used to hide the bar).

If special tweaks like this are required to make an application present a native titlebar or hide the baked-in titlebar, they'll be noted.

## Other caveats

These color schemes will only work with window decorations that actually support changing the titlebar color based on the current color scheme. If you're using a custom window decoration, it may not support using color scheme colors at all, in which case this repo won't be useful to you. See [this KDE Discuss thread](https://discuss.kde.org/t/titlebar-color-change/17231/14) for more information about the interaction between window decorations, color schemes, and custom application styles.

## License

[CC0 - Public Domain](/LICENSE)
