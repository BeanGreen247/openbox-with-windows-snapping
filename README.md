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
