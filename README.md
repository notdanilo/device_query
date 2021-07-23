# device_query

[![Build Status](https://travis-ci.org/ostrosco/device_query.svg?branch=master)](https://travis-ci.org/ostrosco/device_query)

A simple library to query mouse and keyboard inputs on demand without a window.
Will work in Windows, Linux on X11, and macOS.

```Rust
use device_query::{DeviceQuery, DeviceState, MouseState, Keycode};

let device_state = DeviceState::new();
let mouse: MouseState = device_state.get_mouse();
println!("Current Mouse Coordinates: {:?}", mouse.coords);
let keys: Vec<Keycode> = device_state.get_keys();
println!("Is A pressed? {}", keys.contains(Keycode::A));
```

# Dependencies

Windows shouldn't require any special software to be installed for `device_query` to work properly.
On Linux, the X11 development libraries are required for `device_query` to query state from the OS.

On Ubuntu/Debian:
```
sudo apt install libx11-dev
```

On Fedora/RHEL/CentOS:
```
sudo dnf install xorg-x11-server-devel
```

On newer versions of MacOS, you may run into issues where you only see meta keys such as shift,
backspace, et cetera. This is due to a permission issue. To work around this:

* open the MacOS system preferences
* go to Security -> Privacy
* scroll down to Accessbility and unlock it
* add the app that is using `device_query` (such as your terminal) to the list
