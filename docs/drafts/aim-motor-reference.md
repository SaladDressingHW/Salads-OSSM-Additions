# AIM motor technical reference and bench record

[All guides](README.md) · [Main motor setup guide](aim-motor-setup.md)

> **Advanced reference, not universal motor settings or machine commissioning.**
> Start with the main guide's hardware identification, wiring and isolated-bench precautions. The measured results below cover **one 60AIM40F RS485 motor**, not every 57AIM30/60AIM40F revision or controller firmware. Operating-system setup belongs in the [Windows](computer-setup-windows.md) and [Linux](computer-setup-linux.md) FAQs.

Register addresses in this document are **zero-based hexadecimal Modbus protocol addresses**; values are decimal. Check your client's addressing convention before writing. Back up settings, use bounded timeouts, and validate response address, function, frame length and CRC. Recognise Modbus exception responses; receiving bytes alone is not successful communication.

## 1. Programmer behaviour

The inspected [armpitMFG tool](https://armpitmfg.com/ossm/gmp/) opens the port at **19200 / 8N1**, targeting **address 1**. Its “Connected to motor” message only establishes that the USB serial port opened. Editable preset fields are separate from the actual **Read Registers** results. A sent-command message is not a write acknowledgement; **UNSUPPORTED** is not automatically a motor alarm.

The inspected [live receive code](https://armpitmfg.com/ossm/gmp/script.js) has **no receive timeout**. It waits for at least seven bytes for a read or eight for a write; a five-byte Modbus exception can leave it waiting. A stuck message does not distinguish no reply, wrong communication settings or an unhandled exception. The live implementation can change.

For diagnosis, use a client that checks the full response and times out. Do not weaken CRC checks or repeatedly click Write because a read is stuck. The website is a parameter programmer, not a controller flasher or mechanical calibration tool.

## 2. Writing and saving basic settings

First confirm that the [five basic Gold Motor targets](aim-motor-setup.md#5-standard-gold-motor-settings) suit the exact motor and intended firmware. Do not write a full register dump or unrelated advanced fields.

The pinned [KinkyMakers write handler][km-write] does this:

1. Enable Modbus control: **0x00 = 1**.
2. Disable drive output: **0x01 = 0**.
3. Write the five basic settings, then **0x14 = 1** to save parameters.
4. Repeat that settings-and-save pass **three times**.
5. Re-enable drive output with **0x01 = 1**, then read registers.

The source describes repetition as a reliability workaround with an unresolved root cause. It does not prove that every motor drops writes, and it does not replace readback or persistence checks.

The bench test followed the same preparation order and three settings/save passes, checking acknowledgements and per-register readbacks. It deliberately **omitted automatic output re-enable**, then verified settings after an operator-controlled complete power cycle. Do not silently equate that test with the website's output handling.

### Unexpected disable readback

In the tested motor, writing 0x01 = 0 **before enabling Modbus control** returned a valid response/readback of **6**, from an initial **7**. Enabling Modbus first, then disabling output, produced exact acknowledgements and readback **0**.

Do not reverse those operations, generalise 6 as a safe disabled state, or guess all bits in startup value 7. Stop on unexpected responses. After power-up, assume the motor may be energised/holding even when it reports zero speed; never test its shaft by hand.

## 3. Returning from OSSM-rs: advanced baud restoration

> **For a competent operator using a checked Modbus client on an isolated, secured, unloaded motor.** Confirm that the exact motor supports this vendor sequence. Keep the controller signal cable disconnected, people clear and a reachable power cutoff. Mode changes and restarts can energise the motor without a movement command. This is not a sequence to paste into arbitrary advanced fields or a terminal.

### Diagnose and back up first

The pinned OSSM-rs [RS485 provisioning path][rs-provision] probes its target **115200 baud**, falls back to stock **19200**, programs 115200 persistently, and requests a motor power cycle. Its default address is **1**. This describes that implementation, not every board build or the separate step/direction driver.

A motor may retain 115200 after the controller is replaced or reflashed. The standard website still opens at 19200; a successful browser connection can therefore coexist with no motor replies.

1. Close the browser tab to release the port.
2. Use a timeout-bounded, **read-only** client at **115200 / 8N1 / address 1**.
3. Read device-address register **0x15** and alarm register **0x0E**, validating replies.
4. If that fails, also check **19200** read-only. Do not sweep writes through guessed addresses or baud rates.
5. Back up all supported registers before changing anything. Dumps include telemetry as well as settings: **never replay the entire dump as writes**.

The tested motor returned CRC-valid reads at 115200 with address 1 and alarm 0. That established working communication and explained the website's failure. Editing a local website to open at 115200 changes only the computer connection, not the motor's stored baud.

### Vendor-specific restoration sequence

The sequence comes from [OSSM-rs baud setup][rs-baud] and its [baud-code enum][rs-rates]. **801 is the decimal code for 19200 baud**, not the baud rate itself.

1. Connect at the motor's verified current speed (115200 in this test). Confirm identity, no alarm and no motion.
2. Write **0x00 = 1**, then **0x01 = 0**, checking responses/readbacks. Stop on unexpected responses; do not guess that an unknown state is safe.
3. Write **0x03 = 801** and verify it.
4. Write **0x04 = 129** and verify it.
5. Write **0x00 = 506 once** to apply baud provisioning.
6. Close/release the port and complete a power cycle: motor supply off, USB unplugged, allow power to discharge, USB reconnected, motor supply on. Keep the controller disconnected.
7. Reconnect at **19200 / 8N1 / address 1** and read registers again.

These are vendor-specific operations, **not generic Modbus settings**. Do not interrupt the sequence with unrelated writes or save its temporary values as tuning. The special 0x00 = 506 operation persists the baud change for the next restart; the sequence **does not call 0x14 = 1**, the ordinary tuning-save operation. Do not assume restarting undoes the applied baud change.

The source expects the final apply command to give **no response** and tolerates its error. The tested motor instead acknowledged 506. **Either outcome still requires post-restart verification.** Do not endlessly repeat the apply command after a timeout.

Registers **0x03** and **0x04** normally hold acceleration and weak-magnetic-angle settings. In this motor they returned to the backed-up values **50000** and **495** after restart. Check them against **your own backup before any tuning save**. If they remain at 801/129, stop and obtain the correct restoration procedure; never blindly save those temporary values as operating settings.

If 19200 gives no reply after restarting, release the port and probe the previous **115200 read-only**. Report the last acknowledged operation and raw response to a knowledgeable maintainer/vendor instead of repeating the special sequence blindly.

### Finish and verify

Once 19200 and normal register state are verified:

1. Apply the approved five basic targets using the preparation order and three passes in section 2.
2. Check actual readbacks and save acknowledgements. Preserve unrelated advanced values, alarm registers, position targets and device-address fields.
3. Power-cycle again and verify persistence.
4. Confirm startup control mode suits the intended standard firmware. In the tested motor, 0x00 returned to **0**, 0x01 to **7**, and specific-function 0x19 to **0**. These are observations, not values to force onto every revision.
5. Verify no alarm and no unexpected motion. Disconnect the programmer and check controller firmware before reconnecting its signals with power off.

Do not reconnect an OSSM-rs controller during migration; its startup provisioning can change the baud again. Returning to OSSM-rs later is a separate setup operation. This record does not establish its correct gearing, tuning or firmware configuration for your build.

## 4. Single-motor verification record

This is one measured migration, **not a factory specification or required starting state**. Register exchanges used bounded timeouts, validated responses/CRC and durable backups.

| Item | Before migration | After final power cycle |
| --- | ---: | ---: |
| Baud | 115200 | **19200** |
| Device address (0x15) | 1 | **1** |
| Gear denominator (0x0B) | 8192 | **800** |
| Gear numerator (0x0A) | 32768 | **32768**, unchanged |
| Speed proportional gain (0x05) | 5000 | **3000** |
| Position proportional gain (0x07) | 5000 | **3000** |
| Direction polarity (0x09) | 1 | **1** |
| Standstill maximum output (0x18) | 506 | **600** |
| Acceleration (0x03) | 50000 | **50000** |
| Weak magnetic angle (0x04) | 495 | **495** |
| Alarm (0x0E) | 0 | **0** |
| Reported speed (0x10) | 0 | **0** |

Three settings/save passes were acknowledged and read back. A separate read-only scan after the final power cycle verified the targets. **No position, homing or run commands were sent. Controller firmware installation and machine motion were not verified.** The initial values are what this motor contained; do not assume OSSM-rs wrote all of them.

For your own records, save the date, motor label/variant, intended firmware/version, adapter identity, original baud/address and register dump, exact changes/replies, and the post-power-cycle dump. Keep them in a durable location, not a temporary folder.

## 5. What still needs confirmation

- Supported motor revisions and controller/firmware combinations.
- The 60AIMxxF datasheet's conflicting supply label, resolved for the purchased variant.
- Complete controller wiring, motion scaling, first-power-on, homing and stop procedures.
- The provisional startup direction described in the [main guide](aim-motor-setup.md#startup-direction-and-orientation).

The source conversation described “forward motion first”, followed by “in”. A follow-up interpreted that as “extend first”, polarity 1, clockwise from the PCB side and the 24 mm adapter on the right. The excerpt does not confirm that interpretation or clearly identify the view; “in” could also mean retraction. A labelled view and physical verification are required before turning it into instructions. Never equate direction polarity with DC supply polarity.

## Sources

The pinned tool and driver sources describe the inspected implementations, not every release:

- [KinkyMakers tool instructions][km-tool], [basic defaults][km-defaults], [write/save handler][km-write] and [connection settings][km-connect].
- [OSSM-rs address/baud codes][rs-rates], [baud setup][rs-baud] and [startup provisioning][rs-provision].
- [Older AIM manual][aim-manual] for register descriptions; do not substitute it for an exact-revision wiring/rating manual.
- [armpitMFG live script](https://armpitmfg.com/ossm/gmp/script.js) for the observed UI and receive-loop behaviour; this source is not version-pinned.

[km-tool]: https://github.com/KinkyMakers/OSSM-hardware/blob/b7f01bf6df1be6f3ebf17dc0e31ed64ddf4c15b7/Hardware/Servo%20Tools/Gold%20Motor/README.md
[km-defaults]: https://github.com/KinkyMakers/OSSM-hardware/blob/b7f01bf6df1be6f3ebf17dc0e31ed64ddf4c15b7/Hardware/Servo%20Tools/Gold%20Motor/GMP/index.html#L229-L255
[km-write]: https://github.com/KinkyMakers/OSSM-hardware/blob/b7f01bf6df1be6f3ebf17dc0e31ed64ddf4c15b7/Hardware/Servo%20Tools/Gold%20Motor/GMP/script.js#L59-L123
[km-connect]: https://github.com/KinkyMakers/OSSM-hardware/blob/b7f01bf6df1be6f3ebf17dc0e31ed64ddf4c15b7/Hardware/Servo%20Tools/Gold%20Motor/GMP/script.js#L6-L24
[rs-rates]: https://github.com/ossm-rs/ossm/blob/4e72bdcacd7a28a33bdf432f57228a9878316731/drivers/m57aim/src/lib.rs#L59-L89
[rs-baud]: https://github.com/ossm-rs/ossm/blob/4e72bdcacd7a28a33bdf432f57228a9878316731/drivers/m57aim/src/rs485.rs#L104-L118
[rs-provision]: https://github.com/ossm-rs/ossm/blob/4e72bdcacd7a28a33bdf432f57228a9878316731/drivers/m57aim/src/rs485.rs#L170-L222
[aim-manual]: https://github.com/KinkyMakers/OSSM-hardware/blob/b7f01bf6df1be6f3ebf17dc0e31ed64ddf4c15b7/Hardware/Servo%20Tools/Gold%20Motor/YZ-AIMManual_v2_55.pdf
