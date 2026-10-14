# AIM motor setup: new motors and returning from OSSM-rs

> **WIP: motor-side bench setup, not a complete machine commissioning guide.**
> Check your exact motor, connector, controller and firmware before using these settings. Successful register reads do not prove correct machine direction, travel, assembly or safety.

[All guides](README.md) · [Capstan XL HG20](capstan-xl-hg20.md)

## 1. Choose the right setup

This guide covers the **57AIM30 Gold Motor** workflow and one **60AIM40F RS485** bench migration. It does not establish compatibility for every motor revision.

| Your situation | What to do |
| --- | --- |
| New, unprogrammed RS485 AIM motor | Identify the hardware, connect safely, back up its settings, then apply the approved configuration |
| Gold Motor supplied preconfigured by Research and Desire | Verify its settings; do not reset it unnecessarily |
| Previously used OSSM-rs; switching to standard KinkyMakers/R&D firmware | Read [Returning from OSSM-rs](#6-returning-from-ossm-rs) before using the programmer |
| Keeping OSSM-rs | Follow that firmware's instructions; do not apply this migration |

**The controller board and its firmware are different things.** Confirm what is installed. Reflashing the controller does not necessarily undo settings stored inside the motor.

### Check the motor and supply

- **57AIM30:** use its exact label and manual. The Gold Motor guide describes 20–36 V DC; that is not a universal AIM-series rating.
- **60AIM40F:** the Capstan BOM specifies the **RS485 single-turn version**, not CAN, and a **36 V, 5 A+** supply. The 60AIMxxF-EN datasheet's rating table says **36 V DC ±10%**, but its power-terminal drawing says +24V. Resolve that conflict with the label/vendor before powering your motor.
- One 60AIM40F was configured and checked after power cycles. No 57AIM30 bench test is documented here. The [technical reference](aim-motor-reference.md) records the tested motor's results and limitations.

## 2. Equipment and safe connection

You need a **USB–RS485 adapter** (not USB–TTL/UART or USB–RS232), a verified programming lead, the motor's correctly rated supply, a Web Serial-capable desktop browser, and a way to save the original settings. USB does not power the motor itself.

**Before writing settings:** secure the motor, leave its shaft unloaded and disconnected from the mechanism, disconnect the OSSM controller's signal cable, keep people clear, and have a reachable power cutoff. Mode changes and restarts can energise the motor without a movement command. Never test a powered shaft with your fingers; zero reported speed does not mean zero torque.

### Connection sequence

1. Turn the motor supply off and unplug the USB adapter.
2. Disconnect the controller's signal cable so it cannot command the motor during programming.
3. Connect verified RS485 data, communication ground and any required interface supply.
4. Plug in USB, then apply the motor's normal DC supply.
5. Turn motor power off and unplug USB **before changing any wiring**.

For a complete power cycle: motor supply off → USB unplugged → allow power to discharge → USB reconnected → motor supply on. Leave the controller signal cable disconnected during verification.

### Verify the connector view

For the **10-pin RS485 socket shown on p. 3 of the 60AIMxxF-EN datasheet**, face the motor socket with its latch/key at the top as drawn:

```text
                    latch/key

Upper row:  6 COM/GND   7 WR   8 RDY/PF   9 ZO   10 +5V
Lower row:  1 NC        2 A    3 B        4 EN+   5 EN-
```

| Motor pin | Programming connection |
| --- | --- |
| 2: 485A | Adapter RS485 A |
| 3: 485B | Adapter RS485 B |
| 6: COM | Adapter communication GND/reference |
| 10: 485_5V | Verified external **5 V interface supply**, as required by the manual |

**Pin 10 is not the motor power input. Never connect 24 V or 36 V to it.** The datasheet requires external 5 V for this communication interface; motor power alone does not prove that the RS485 side is powered.

Check whether the adapter's 5V terminal is an output or an input; do not join two powered outputs. Wire colours do not establish function. The cable's wire-entry view is mirrored relative to this socket view. Verify your actual connector: the older AIM manual shows the same numbered functions, but that does not establish the connector on every revision. CAN wiring is different.

## 3. Connect your computer

These steps apply regardless of your operating system:

1. Connect the USB adapter and confirm your computer recognises it. If a driver is needed, use the adapter manufacturer's driver for its actual chip.
2. Open the [Gold Motor Programming tool](https://armpitmfg.com/ossm/gmp/) in a Web Serial-capable desktop browser, such as Chrome, Chromium or Edge. Support depends on the browser and platform; a missing serial chooser is not a motor fault.
3. Close other serial applications and programming tabs. Only one application should use the adapter at a time.
4. Click **Connect to Motor** and select the USB adapter. Port names vary; do not copy a port name from somebody else's setup.
5. **Read and save actual motor settings before writing anything.** If the motor previously ran OSSM-rs, check section 6 first.

If the adapter is missing or access is denied, use the optional [Windows FAQ](computer-setup-windows.md) or [Linux FAQ](computer-setup-linux.md). For other systems, check your adapter manufacturer's and browser's documentation. The electrical connection and motor settings do not change just because the computer is different.

## 4. Understand the programmer

The website programs motor parameters. It does **not** flash the OSSM controller or validate the assembled machine.

The linked tool opens at **19200 baud, 8 data bits, no parity, 1 stop bit (8N1)** and targets **device address 1**. These describe the inspected tool version, not every motor's current configuration.

- **Connected to motor** means the computer opened the serial port, not that the motor replied.
- Editable fields may contain presets rather than settings read from your motor.
- **Sent read/write command** means a request was sent, not necessarily acknowledged.
- **Read Registers** displays the actual register results. Use those for verification.
- A stuck read or an **UNSUPPORTED** label does not by itself identify a wiring fault or motor alarm.

If reads fail, stop. Do not repeatedly click Write or reset the motor to guess at a fix. Advanced diagnosis needs a client with timeouts and response/address/function/CRC checks; see the [technical reference](aim-motor-reference.md).

## 5. Standard Gold Motor settings

These are the **five basic defaults in the linked KinkyMakers tool**, not a factory reset or universal settings for every AIM motor. Confirm compatibility with your motor and intended controller firmware first.

Addresses below are **zero-based Modbus protocol addresses in hexadecimal**; values are decimal. For example, 0x0B is address 11 decimal, not a 4xxxx display label. Check your client's addressing convention before any write.

| Register | Setting | Value |
| --- | --- | ---: |
| 0x0B | Electronic gear denominator / tool label “Steps per Revolution” | **800** |
| 0x18 | Standstill maximum allowed output | **600** |
| 0x05 | Speed-loop proportional gain | **3000** |
| 0x07 | Position-loop proportional gain | **3000** |
| 0x09 | Direction polarity | **1** |

**600 is a register encoding, not 600 A or 600%.** The older manual describes additional behaviour in its last decimal digit. Do not substitute guessed current limits. The gear denominator also depends on the numerator and controller scaling; the tested motor had 0x0A = 32768. Do not blindly apply its gearing to another revision.

### Read, configure and verify

1. Identify the motor and intended firmware, then prepare the isolated bench setup.
2. Connect at **19200 / 8N1 / address 1** and save actual register reads. If reads fail, troubleshoot before writing.
3. Compare the five approved targets with your backup; preserve unrelated settings.
4. Keep the web tool's advanced fields hidden, check its version and basic settings, then use **Write Settings once**. The published implementation re-enables drive output at the end: keep clear throughout.
5. Read the actual registers back, power-cycle, and read again to confirm persistence.
6. Only then proceed to controller setup and the separate commissioning procedure.

The official tool enables Modbus control, disables output, writes/saves the basic settings in **three passes**, then re-enables output. The repetition is a documented workaround, not a substitute for readback. For manual clients, the exact order and the tested procedure's different output handling are in the [technical reference](aim-motor-reference.md#2-writing-and-saving-basic-settings). Do not improvise register writes.

## 6. Returning from OSSM-rs

The linked OSSM-rs RS485 driver can persistently change the motor from **19200 to 115200 baud**. A motor may stay at 115200 after the controller is replaced or reflashed. The standard web tool can then open the USB adapter but receive no motor replies.

Close the browser tab and have a competent operator use a timeout-bounded, **read-only** Modbus client to check **115200 / 8N1 / address 1**, then 19200 if needed. Back up supported registers and verify responses before making changes. A dump contains live telemetry as well as settings: **never replay the whole dump as writes**.

The [advanced baud-restoration procedure](aim-motor-reference.md#3-returning-from-ossm-rs-advanced-baud-restoration) uses a vendor-specific sequence and was tested on one 60AIM40F. It is not a command to paste into a terminal or arbitrary advanced fields. Confirm motor compatibility and use the isolated bench setup before following it.

Changing a local website's connection speed only changes the computer side; it does not restore the motor's stored baud rate. Keep the OSSM-rs controller disconnected throughout migration, since its startup provisioning may change the baud again.

## 7. Troubleshooting

| Symptom | Check next |
| --- | --- |
| Adapter missing from the chooser | USB detection, matching adapter driver and browser support; see the computer FAQs |
| Failed to open serial port | Computer access permissions, another application using it, or browser restrictions |
| Connected, but no actual reads | Motor/interface power, verified A/B and ground, baud/address; check 115200 after OSSM-rs use |
| Read command never finishes | Use a timeout-capable client; no response and an unhandled exception can look alike |
| Garbled or CRC-invalid replies | Baud/framing, bus contention, adapter type, noise and verified wiring; do not accept invalid replies |
| Settings disappear after restarting | Save acknowledgement and post-power-cycle readback; stop after bounded failure rather than repeatedly writing EEPROM |
| Communication works but homing/scaling is wrong | Stop motion; controller firmware and mechanical commissioning are separate from programming |

Adapter LEDs commonly show traffic, not continuous connection. A/B labels can differ between vendors; only swap the data pair when verified documentation justifies it, with motor power off and USB disconnected. Never experiment with supply or ground pins.

## 8. Reconnect and commission

1. Turn motor power off, unplug USB and remove the programming connections.
2. Confirm the controller board/firmware, gearing and Capstan-specific motion scaling before reconnecting its signals with power off.
3. Follow a maintainer-approved first-power-on/homing procedure with clear travel, no operating load, people clear and a reachable power cutoff.
4. Stop immediately if direction, homing, scale or travel is wrong. Do not increase force or bypass limits to compensate.

**The complete commissioning procedure is still missing.** The motor's 800 setting alone does not validate drum circumference or travel. A register-only test does not establish correct motion or safe stopping.

### Startup direction and orientation

**Not yet verified:** extension-first startup, clockwise rotation viewed from the PCB side, and the 24 mm adapter on the right in that view. The available conversation is ambiguous about “forward”/“in”, and does not identify an unambiguous viewpoint. Do not position an attachment or choose a homing direction from it.

The documented default **0x09 = 1** does not prove physical direction. Looking from the opposite end reverses apparent rotation, and “PCB side” must not be assumed to mean the rear motor connector side. Direction polarity is **not DC supply polarity**: never reverse supply leads to change motion direction.

## Sources and further detail

- [Technical reference and single-motor bench record](aim-motor-reference.md): tool behaviour, manual write order, advanced migration and measured results.
- Computer setup FAQs: [Windows](computer-setup-windows.md) · [Linux](computer-setup-linux.md).
- [KinkyMakers Gold Motor connection instructions][km-tool], [basic defaults][km-defaults] and [write/save implementation][km-write].
- [OSSM-rs startup provisioning][rs-provision]. This describes the pinned RS485 implementation, not every build or its separate step/direction path.
- [Motor datasheet folder](https://drive.google.com/drive/folders/1GZ72pyu7kxIsglAycxUcyNT6uF8lkAtw) and [60AIMxxF-EN.pdf](https://drive.google.com/file/d/1peHYBlGcQaxfkdXuoFrp-RSuasO20YCF/view): ratings p. 2, connector views p. 3; hosted documents are not version-pinned.
- [Older AIM register manual][aim-manual]; use your exact-revision manual for wiring and ratings.
- [Capstan parts and supply guidance](../../Capstan%20OSSM%20XL/Assembly%20Guide%20%28WIP%29/2.%20Tools%20And%20Parts.md).

[km-tool]: https://github.com/KinkyMakers/OSSM-hardware/blob/b7f01bf6df1be6f3ebf17dc0e31ed64ddf4c15b7/Hardware/Servo%20Tools/Gold%20Motor/README.md
[km-defaults]: https://github.com/KinkyMakers/OSSM-hardware/blob/b7f01bf6df1be6f3ebf17dc0e31ed64ddf4c15b7/Hardware/Servo%20Tools/Gold%20Motor/GMP/index.html#L229-L255
[km-write]: https://github.com/KinkyMakers/OSSM-hardware/blob/b7f01bf6df1be6f3ebf17dc0e31ed64ddf4c15b7/Hardware/Servo%20Tools/Gold%20Motor/GMP/script.js#L59-L123
[rs-provision]: https://github.com/ossm-rs/ossm/blob/4e72bdcacd7a28a33bdf432f57228a9878316731/drivers/m57aim/src/rs485.rs#L170-L222
[aim-manual]: https://github.com/KinkyMakers/OSSM-hardware/blob/b7f01bf6df1be6f3ebf17dc0e31ed64ddf4c15b7/Hardware/Servo%20Tools/Gold%20Motor/YZ-AIMManual_v2_55.pdf
