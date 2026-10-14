# Linux computer setup FAQ

[All guides](README.md) · [Motor setup](aim-motor-setup.md) · [Windows FAQ](computer-setup-windows.md)

Use this page only if Linux cannot find or open your USB–RS485 adapter. It covers **computer-side access**, not motor wiring, voltage, baud migration or machine commissioning. Follow the main motor guide for those steps.

Distributions and browser packages differ. Device paths and groups below are examples, not required settings for every reader. Do not run the browser as root or change motor parameters to fix a computer-side access error.

## Is the adapter detected?

Connect the adapter to a USB port. Common CH340, CP210x and FTDI adapters usually have kernel drivers already available. Check your system's device information or, if these commands are installed, use:

```sh
lsusb
ls -l /dev/serial/by-id/ /dev/ttyUSB* /dev/ttyACM* 2>/dev/null
```

Compare the list before and after connecting. A USB adapter often appears as `/dev/ttyUSB0` or `/dev/ttyACM0`, but the number can change. When available, a `/dev/serial/by-id/` link is useful for command-line tools. A list of `ttyS…` ports is not proof that any of them is your USB adapter.

If nothing appears, check the USB port, the removable cable's data capability and the adapter manufacturer's instructions. Do not start writing motor settings to diagnose missing USB detection.

## The port exists, but access is denied

Check the actual port's ownership and permissions:

```sh
ls -l /dev/ttyUSB0
```

Replace `/dev/ttyUSB0` with **your detected device**. Your distribution may grant serial access through a device group or a desktop-session rule. Common group names include `dialout` and `uucp`; neither is universal.

If your distribution recommends group-based access, add your account to the **actual serial-device group**, not a guessed group:

```sh
# Replace SERIAL_GROUP with the device group confirmed for your distribution.
sudo usermod -aG SERIAL_GROUP "$USER"
```

Log out fully and log back in, then reopen the browser. Existing browser processes may retain the old group membership. On a managed computer, ask the administrator instead of changing access rules yourself.

### Optional temporary access

If the system supports ACLs and you cannot end your session, grant only your account temporary access to the confirmed port:

```sh
# Example only: use your detected device path.
sudo setfacl -m u:"$USER":rw /dev/ttyUSB0
```

Reopen the browser's serial chooser. Unplugging/replugging the adapter can remove this ACL. If `setfacl` is unavailable, use your distribution's documented access method; installing it is not a motor-programming requirement.

Do not use blanket `chmod 666`, permanent world-writable device rules, or a root browser as a workaround.

## Is another application using the port?

Close other serial tools and programming tabs. If available, check which process owns the actual device:

```sh
fuser -v /dev/ttyUSB0
```

Use your device path. Close the identified application normally rather than killing unfamiliar processes. A browser tab may keep a port open until it is closed.

## The browser still cannot open it

Use a desktop browser with Web Serial support, such as Chrome or Chromium. Verify support for the actual browser build. Sandboxed browser packages can need separate device permissions; follow that package's documentation rather than weakening the sandbox globally.

An open-port error is a computer-side problem first. Once the port opens, return to the [main motor guide](aim-motor-setup.md#4-understand-the-programmer): opening the adapter does not prove that the motor replied.
