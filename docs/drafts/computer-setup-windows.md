# Windows computer setup FAQ

[All guides](README.md) · [Motor setup](aim-motor-setup.md) · [Linux FAQ](computer-setup-linux.md)

Use this page only if Windows cannot find or open your USB–RS485 adapter. It covers **computer-side access**, not motor wiring, voltage, baud migration or machine commissioning. Follow the main motor guide for those steps.

Port names, drivers and menu labels vary with the adapter and Windows version. You can check USB detection with the adapter disconnected from the motor and motor power off.

## Does the adapter need a driver?

The driver is for the **USB adapter**, not the motor. Windows may install a suitable driver automatically. Identify the adapter's chip or model before installing anything; an RS485 connector does not identify its USB chip.

For a **CH340/CH341-based adapter**, use the [official WCH Windows driver](https://www.wch-ic.com/downloads/CH341SER_EXE.html) if Windows has not already installed a working one. Follow the installer instructions and restart only if prompted. For CP210x, FTDI or another chip, use the matching manufacturer's driver instead.

Avoid unrelated driver bundles. On a managed computer, ask the administrator before installing drivers.

## Which port should I select?

1. Plug in the adapter.
2. Open **Device Manager**, for example by searching for it from Start.
3. Expand **Ports (COM & LPT)**. Find the adapter without a warning icon; compare the list before and after connecting if needed.
4. Note its COM number. `USB-SERIAL CH340 (COM3)` is an example, not the port every user should select.
5. Follow the main guide's safe motor connection sequence, open the programmer in a Web Serial-capable desktop browser such as Chrome or Edge, and select that adapter in the browser chooser.

Read and back up the actual settings before writing. If the motor previously used OSSM-rs, read [Returning from OSSM-rs](aim-motor-setup.md#6-returning-from-ossm-rs) first; a correct COM port does not resolve a baud mismatch.

## No COM port appears

- Check Device Manager for a warning or an entry under **Other devices**.
- Confirm the driver matches the adapter's chip/model.
- Try another USB port and, if the lead is removable, a known data-capable cable.
- Check the adapter manufacturer's instructions if it still does not appear.

Resolve USB detection before changing motor wiring or parameters.

## The port appears, but the browser cannot open it

Close other serial applications and programming tabs; only one application should use the adapter at a time. Disconnect/reconnect the adapter and select its current COM port again. Reopen the browser if it retains an old connection.

Verify Web Serial support for your browser/version. Browser or organisation policy may block serial access even when Device Manager shows a working port; check the relevant policy or ask the administrator. Do not disable security controls globally to guess at a fix.

## It connects, but the motor does not reply

A browser connection establishes access to the USB adapter, not communication with the motor. Return to the [main motor troubleshooting table](aim-motor-setup.md#7-troubleshooting) to check motor/interface power, verified wiring and the actual baud/address. Do not reset the motor or repeatedly write settings because a read is stuck.
