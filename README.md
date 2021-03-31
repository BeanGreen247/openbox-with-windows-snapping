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
> add keyboard shortcuts for windows tiling

## BUGS I FOUND
> ~~Opening more than 4 terminal emulators in one go, like running at the same time, causes openbox to crash and logs the user out~~
> 
> Opening more than 8 terminal emulators in one go, like running at the same time, causes openbox to crash and logs the user out

## NOTE

This project is made as a passtime activity and may not be updated all the time.

## Youtube links

[Main video](https://youtu.be/2yxb1ed1lJQ)

[Small update video](https://youtu.be/yt2VVqcNcVY)
