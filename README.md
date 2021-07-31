# openbox-with-windows-snapping
### Basic info
Patched version of the openbox window manager with the window snap feature similar to Aero snap on Windows.

Usage:
```
git clone https://github.com/BeanGreen247/openbox-with-windows-snapping
cd openbox-with-windows-snapping
./configure --prefix=/usr --sysconfdir=/etc --libdir=/usr/lib64
make
sudo make install
```
Multiple monitors kinda work, but it's buggy.

## TO-DO
> fix screen sharing bug when Two or more monitors present (shows both monitors instead of the selected one, does not happen in obs)
>
> fix snapping of apps when Two or more monitors present (snapping works fully on main monitor, but you can only snap to the top to maximize on the second monitor)
>
> ~~fix performance problems~~ (some may still exist,but I have not noticed them)
>
> ~~add keyboard shortcuts for windows tiling~~ see [Window Tiling](#window-tiling) [!warning!](#bugs-i-found)

## BUGS I FOUND
> ~~Opening more than 4 terminal emulators in one go, like running at the same time, causes openbox to crash and logs the user out~~
> 
> Opening more than 8 terminal emulators in one go, like running at the same time, causes openbox to crash and logs the user out
> 
> warning, window tiling causes all windows to tile no matter what monitor, unless they are on the same monitor

## NOTE

This project is made as a passtime activity and may not be updated all the time.

## Make sure to have these packages installed
* libglib2.0
* libpango1.0-dev
* libxml2-dev
* automake
* perl

## Aditional dependencies cam be installed like this
```
sudo apt install libcpan-distnameinfo-perl libcpan-meta-check-perl libfile-pushd-perl libmodule-build-perl liblocal-lib-perl libmodule-cpanfile-perl libparse-pmfile-perl libstring-shellquote-perl libpango-perl libgtk2-perl cpanminus
```
## May need to do
```
git clone https://github.com/trizen/Linux-DesktopFiles
cd Linux-DesktopFiles
cpan Module::Build
perl Build.PL
perl ./Build
perl ./Build test
perl ./Build install
sudo cpanm Linux::DesktopFiles
sudo cpanm Data::Dump
```

## Dynamic menu
```
git clone git://github.com/trizen/obmenu-generator
sudo cp obmenu-generator/obmenu-generator /usr/bin
```
edit the schema.pl file for custom defaults then do the following
```
mkdir ~/.config/obmenu-generator
cp -r obmenu-generator/schema.pl ~/.config/obmenu-generator/
obmenu-generator -p
```

## Recommendation
To make it easier to use install these packages
* dmenu //not requried but cool to have
* vala-panel //a simple panel

## Suggestion
After running the configure commad I would recommend to do this change in the Makefile before running make from this
```
CFLAGS = -g -O2 -DNDEBUG -DG_DISABLE_ASSERT -fno-strict-aliasing
```
to this
```
CFLAGS = -g -O3 -DNDEBUG -DG_DISABLE_ASSERT -fno-strict-aliasing
```
or this
```
CFLAGS = -g -Ofast -DNDEBUG -DG_DISABLE_ASSERT -fno-strict-aliasing
```
It may or may not give a small performance boost.

For more info go [here](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html).

## Youtube links

[Main video](https://youtu.be/2yxb1ed1lJQ)

[Small update video](https://youtu.be/yt2VVqcNcVY)

## Window Tiling
Add this to your rc.xml file somewhere in the keybind section
```
<!-- Window tiling -->
    <!-- Switch tiling -->
    <keybind key="W-m">
      <action name="If">
        <query target="default">
          <maximizedvertical>yes</maximizedvertical>
        </query>
        <!-- Switch to horizontal -->
        <then>
          <action name="UnmaximizeFull"/>
          <action name="MoveResizeTo">
            <height>50%</height>
          </action>
          <action name="MaximizeHorz"/>
          <action name="MoveResizeTo">
            <x>0</x>
            <y>0</y>
          </action>
          <action name="NextWindow">
            <interactive>no</interactive>
            <dialog>none</dialog>
            <finalactions>
              <action name="UnmaximizeFull"/>
              <action name="MoveResizeTo">
                <height>50%</height>
              </action>
              <action name="MaximizeHorz"/>
              <action name="MoveResizeTo">
                <x>0</x>
                <y>-0</y>
              </action>
            </finalactions>
          </action>
        </then>
        <!-- Switch to vertical -->
        <else>
          <action name="UnmaximizeFull"/>
          <action name="MoveResizeTo">
            <width>50%</width>
          </action>
          <action name="MaximizeVert"/>
          <action name="MoveResizeTo">
            <x>0</x>
            <y>0</y>
          </action>
          <action name="NextWindow">
            <interactive>no</interactive>
            <dialog>none</dialog>
            <finalactions>
              <action name="UnmaximizeFull"/>
              <action name="MoveResizeTo">
                <width>50%</width>
              </action>
              <action name="MaximizeVert"/>
              <action name="MoveResizeTo">
                <x>-0</x>
                <y>0</y>
              </action>
            </finalactions>
          </action>
        </else>
      </action>
     </keybind>
      <!-- Window tiling end -->
    <!-- Keybindings for window switching with the arrow keys -->
    <keybind key="W-S-Right">
      <action name="DirectionalCycleWindows">
        <direction>right</direction>
      </action>
    </keybind>
    <keybind key="W-S-Left">
      <action name="DirectionalCycleWindows">
        <direction>left</direction>
      </action>
    </keybind>
    <keybind key="W-S-Up">
      <action name="DirectionalCycleWindows">
        <direction>up</direction>
      </action>
    </keybind>
    <keybind key="W-S-Down">
      <action name="DirectionalCycleWindows">
        <direction>down</direction>
      </action>
    </keybind>
```
