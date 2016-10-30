<img src=".github/img/logo_thumb.png" alt="Logo" align="left" /> Adapta-gtk-theme
======


An adaptive Gtk+ theme based on Material Design Guidelines.

<img src=".github/img/sunlight.png" alt="Day" align="left" /> **Adapta**:
 * Light/Dark variant Gtk+ 3.22/3.20/3.18 theme
 * Light/Dark variant Budgie-Desktop theme
 * Light variant Gtk+ 2.0 theme
 * Light variant Gnome-Shell theme
 * Light variant Cinnamon theme

<img src=".github/img/moon.png" alt="Night" align="left" /> **Adapta-Nokto**:
 * Light/Dark variant Gtk+ 3.22/3.20/3.18 theme
 * Light/Dark variant Budgie-Desktop theme
 * Dark variant Gtk+ 2.0 theme
 * Dark variant Gnome-Shell theme
 * Dark variant Cinnamon theme

> **Note:**
>
>   Both also include common GNOME-Flashback, Unity7, XFce4, Mate and LXDE theming.

<img src=".github/img/sunlight-eta.png" alt="Day" align="left" /> **Adapta-Eta**:
 * Light/Dark variant Gtk+ 3.22/3.20 theme
 * Light/Dark variant Budgie-Desktop theme

<img src=".github/img/moon-eta.png" alt="Night" align="left" /> **Adapta-Nokto-Eta**:
 * Light/Dark variant Gtk+ 3.22/3.20 theme
 * Light/Dark variant Budgie-Desktop theme

> **Note:**
>
>   Eta is a tiny Gtk+ 3.2x widget variant for saving space (Gtk+ 3.22.x/3.20.x only).
>
>   I suggest you use the Eta variants if your LCD resolution is lower than FHD (1080p).

Elements
--------
![Materials](.github/img/Materials.png)

Required Components
-------------------
Adapta supports Gtk+ 3.22.x, 3.20.x and 3.18.x

 ```
 * Gtk+-3.0             >= 3.22.0 (or 3.20.1 or  3.18.9)
 * Gtk+-2.0             >= 2.24.30
 * gtk2-engines-pixbuf  >= 2.24.30
 * gtk2-engines-murrine >= 0.98.1
 ```

Supported Desktop Environments
------------------------------

 ```
 * GNOME-Shell     >= 3.22.0 (or 3.20.1 or 3.18.3)
 * GNOME-Flashback >= 3.22.0 (or 3.20.1 or 3.18.2)
 * Budgie-Desktop  >= 10.2.5
 * Cinnamon        >= 3.0.1 (or 2.8.6)
 * Unity7          >= 7.4.0
 * XFce4           >= 4.12.2
 * Mate            >= 1.14.0 (Gtk+ 3.2x only)
 * LXDE            >= 0.99.1 (Gtk+ 2.x only)
 ```

 > **Note:**
 >
 >   * Mate-Desktop support is a W.I.P.

Unsupported Gtk+ Based Desktops
-------------------------------
 * Pantheon

Installation from Package(s)
----------------------------
 * AUR: https://aur.archlinux.org/packages/adapta-gtk-theme/ and some others

 * Copr: https://copr.fedorainfracloud.org/coprs/heikoada/gtk-themes/

 * PPA: https://launchpad.net/~tista/+archive/ubuntu/adapta

 > **Note:**
 >
 >   * Solus OS has an eopkg (ypkg) in main repository.

Installation from Git Source
----------------------------
1. If previous versions were installed/existed, remove them first.

 ```
 sudo rm -rf /usr/share/themes/{Adapta,Adapta-Eta,Adapta-Nokto,Adapta-Nokto-Eta}
 rm -rf ~/.local/share/themes/{Adapta,Adapta-Eta,Adapta-Nokto,Adapta-Nokto-Eta}
 rm -rf ~/.themes/{Adapta,Adapta-Eta,Adapta-Nokto,Adapta-Nokto-Eta}
 ```

2. Check build-requirements:
 Today Adapta bundles neither pre-generated stylesheets nor PNG images.
 So users and/or contributors should generate proper CSSs and PNGs at build-time.

 ```
 * autoconf
 * automake
 * inkscape
 * libglib2.0-dev (glib2)          >= 2.48.0
 * libxml2-utils (libxml2)
 * pkg-config (pkgconfig)
 * ruby-bundler (rubygem-bundler)  >= 1.11
 * ruby-sass (rubygem-sass)        >= 3.4.21
 ```

 > **Note:**
 >
 >   * Adapta employs **Gem** generator for SASS/SCSS via `bundle` and `sass`.
 >   * Adapta uses `inkscape` to generate installable PNG files.
 >   * Adapta uses `glib-compile-resources` to compile gresource file for Gnome-Shell.

3. Build and install system-wide:

 ```
 ./autogen.sh
 make
 sudo make install
 ```

 > **Note:**
 >
 >   * Default prefix is `/usr`.
 >   * `Adapta-Nokto` dark variant is installed as default.
 >   * `make` generates proper CSSs and PNGs to be installed.
 >     It will take about 5min to 15min to build.
 >     For example, Ubuntu's build-server takes 10min.
 >   * `sudo make install` installs multiple versioned theme and Gtk+ automatically selects the properly versioned one when running.

4. To speed up by using concurrency-build, pass this specific option to `autogen.sh`:

 ```
 --enable-parallel       enable parallel-build support (type: bool)
 ```

 > **Note:**
 >
 >   * This feature requires GNU `parallel`, so please add `parallel` to build-requirements.
 >     Parallel can execute multiple scripts and binaries to be suitable for multi-threading.
 >     It could especially shorten the rendering-time via Inkscape and generation-time via sass.
 >   * `-jN` option to be passed to GNU `make` is surely usable, but Adapta currently employs `parallel.
 >   * This feature should not be applied when packaging on remote/shared build-servers.

5. To disable some DE supports, pass these specific options to `autogen.sh`:

 ```
 --disable-cinnamon      disable cinnamon support (type: bool)
 --disable-flashback     disable flashback support (type: bool)
 --disable-unity         disable unity support (type: bool)
 --disable-xfce          disable xfce support (type: bool)
 --disable-mate          disable mate support (type: bool)
 --disable-openbox       disable openbox support (type: bool)
 ```

 > **Note:**
 >
 >   * The installer installs GNOME/Budgie-Desktop support even if all of options above were applied.
 >   * Cinnamon/Unity/Mate support hooks `metacity-1` directory even if GNOME-Flashback support was disabled.

6. To enable next Gtk+ release support, pass this option:

 ```
 --enable-gtk_next      enable Gtk+ 4.0 support (type: bool)
 ```

7. To change the default 5 **Key-Colors**, pass these options:

 ```
 --with-selection_color        Primary color for 'selected-items' (Default: #00BCD4 = Cyan500, type: int)
 --with-second_selection_color Primary color for 'select' effects (Default: #4DD0E1 = Cyan300, type: int)
 --with-accent_color           Secondary color for notifications and OSDs (Default: #4DB6AC = Teal300, type: int)
 --with-suggestion_color       Secondary color for 'suggested' buttons (Default: #009688 = Teal500, type: int)
 --with-destruction_color      Tertiary color for 'destructive' buttons (Default: #FF5252 = RedA200, type: int)
 ```

 > **Note:**
 >
 >   * Color-codes are defined as `#` + 6`HEX`s (Standard RGB definitions in HTML codes).
 >     Uppercases are strongly recommended in Adapta code-base.
 >   * The Material Design Color Palette can be found [here](https://www.google.com/design/spec/style/color.html#color-color-palette).
 >   * Example: If you would like to use 'Teal500' as selection_color, use this:
 >
 >     ```./autogen.sh --with-selection_color=#009688 --with-second_selection_color=#4DB6AC```
 >
 >     This switchese the theme to almost Teal key colors.
 >   * Basically `selection_color` and `suggestion_color` should use `500` colors,
 >     and `second_selection_color` and `accent_color` should use `300` colors.
 >   * While doing `make`, Adapta changes those 5 colors in all stylesheets and images,
 >     and `make clean` cleans up all generated files from source directories.

Extra Browser Support
---------------------
 To try experimental browser specific theming, pass this option:

 ```
 --enable-chrome         enable Chrome(ium) support (type: bool)
 ```

 The compressed `crx` files will be installed into `Adapta/chrome` and `Adapta-Nokto/chrome`.

 > **Note:**
 >
 >   * Currently only Chrome(ium) theming is supported.
 >
 >   * Vivaldi can make custom themes via settings like these:
 >     ```
 >     Background: #FAFBFC (#3E515A)
 >     Foreground: #263238 (#ECEFF1)
 >     Highlight:  #00BCD4
 >     Accent:     #2A373E
 >     Accent Color from Active Page: [ ]
 >     Apply Accent Color to Window:  [*]
 >     Transparent Tabs:              [*]
 >     Corner Rounding:               2px
 >     ```

Extra Dock Support
------------------
 To try "Plank" theming, pass this option:

 ```
 --enable-plank         enable Plank support (type: bool)
 ```

 Then select `Gtk+` via `plank --preferences`.

 > **Note:**
 >
 >   * Both Adapta and Adapta-Nokto shares the same theming.
 >   * Don't expect too much. Plank is NOT a themeable widget for me!

Extra Compositor Support
------------------------
 Compton is the famous stand-alone compositor that works well with the Openbox window-manager. The installer installs recommended configuration file `compton.conf` into `Adapta/openbox-3` directory if Openbox support is enabled.

 Next, copy that file into `~/.config/` and restart compton to read the settings.  That compositor still has some limitations in its features for Adapta, however.

Work in Progress
----------------
* Conversion to Gtk+ 4.0
* Add Mate 1.14 integration

TODO
----
* Prepare for Steam theming (priority: Low)
* Add Firefox specific theming (priority: undecided)

Public License
--------------
 GPLv2

 > **Note:**
 >
 > SVG files are licensed under CC BY-SA 3.0

Special Thanks to
--------------
 Nana-4, the developer of Flat-Plat.
