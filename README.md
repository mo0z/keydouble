![logo](https://github.com/baskerville/keydouble/raw/master/logo/keydouble_logo.png)

---

This little X utility enables the use of keys simultaneously as modifiers and ordinary keys,

The original key behavior is maintained under simple key press/release circumstances; but when a key is chorded, it can act a s a modifier.

E.G. Left shift + b produces B, but left shift tapped on its own might produce leftparen.
## Install

Run

    make; make install

By default, this will install in /usr/local/bin. If you'd like it somewhere else, then copy the executables to your `bin` directory of choice.


## Configuration

`kdlaunch` honors a configuration file at `~/.keydoublerc`.

This file contains *both* xmodmap configuration and keydouble configuration.

An example configuration file is provided at `example/keydoublerc`.

To write your own, use `xev` to discover the natural keycode fo the key you'd like to alter. Then pick an unused keycode (working backwards from 255 is recommended). In `.keydoublerc`'s natart_pairs, add a pair `NATURAL_KEYCODE:UNUSED_KEYCODE` and then add two xmodmap commands: one mapping the natural keycode to the modifier of your choice, and the other mapping the unused keycode to the keysym you'd like to appear when you tap. You may also need to add the keysym to the appropriate modifier (i.e. `add control = Control_L`). See xmodmap's docs for details.

If you have a personal `xmodmap` configuration, copy it into this file, put it at `~/.xmodmaprc` (or change the relevant path in `kdlaunch`).

Once you've tested (try `kdlaunch`) and you're satisfied, add

    kdlaunch &

to `~/.xinitrc`.

To kill `keydouble` run `kdkill`.


## Dependencies

- libxtst
- xorg-xmodmap
- dash


## Strategy

The default keycode (called *natural*) of the original key is mapped to the modifier keysym and the keycode generated by `keydouble` (called *artificial*) under isolated key press/release is mapped to the original keysym.

The mapping is done by `xmodmap` and the *artificial* keycode generation by `keydouble`.


### Troubleshooting.

```Error!   Option "-query" not recognized```

Either upgrade your x utils, or (what may be easier) hardcode your keyboard layout in kdlaunch. There's a comment pointing out where to put it.


If needed (i.e. if you encounter record module errors), the `record` X module can be loaded with:

    Section "Module"
        Load "record"
    EndSection

in `/etc/X11/xorg.conf`.