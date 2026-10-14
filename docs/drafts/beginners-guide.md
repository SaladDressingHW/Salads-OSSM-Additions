# Beginner's guide to the OSSM ecosystem

[All guides](README.md) · [Capstan XL](capstan-xl-hg20.md) · [Shicks mount](shicks-mount-modernised.md)

> **WIP:** this guide helps you plan a build. It does not replace the assembly and operating instructions for your chosen hardware. Some of those instructions are still incomplete; check their status before ordering or building.

## 1. Start with a complete build

Choose one documented drive, then match its mount, controller, firmware, supply and attachments. You do not need every accessory in this repository.

OSSM stands for **Open Source Sex Machine**. The original project combines a motor-driven linear mechanism with adjustable motion control. Start with the [official OSSM hardware repository](https://github.com/KinkyMakers/OSSM-hardware) for the standard build and its requirements.

The additions here include the Capstan OSSM XL drive, Shicks Mount Modernised and several accessories. They are separate projects: choosing a drive doesn't automatically choose your mount, controller, power supply or attachment.

Read the assembly process and make one compatible parts list before buying or printing. The guides do not assume a particular computer or printer; examples and saved profiles must be checked against your own equipment.

## 2. Choose your drive

| Build | Where to read | What to keep in mind |
| --- | --- | --- |
| Standard OSSM | [Official hardware documentation](https://github.com/KinkyMakers/OSSM-hardware) | Follow its own current BOM and instructions. Don't mix in Capstan hardware just because a part has a similar name. |
| Capstan OSSM XL, HG20 | [Project overview][capstan] and [assembly guide](capstan-xl-hg20.md) | The recommended Capstan rail family. Printing and assembly are more involved than the standard build. |
| Existing MGN12H Capstan | [Version comparison][capstan] | Deprecated. The files remain available for existing builds, but this isn't the default route for a new one. |
| Abandoned proof of concept | The abandoned Capstan Proof of Concept folder | A historical experiment, not a current beginner build. |

A stronger motor is not automatically a safer or more suitable choice. Think about compatibility, cost, available instructions, your fabrication experience, and how you'll support and stop the complete machine. **Motor force figures are not safe force limits for a person.** Do not use your body as a load test to choose or validate a machine.

### Before you order

- [ ] Choose one documented build and keep its matching parts list and model files together.
- [ ] Check the exact motor, rail/carriage, controller, firmware and power supply combination.
- [ ] Choose a compatible mount and machine-to-mount interface.
- [ ] Check your print bed, materials, orientation/support requirements and experience level.
- [ ] Budget for the **whole** system: shipping, tax, tools, electronics, mounting and outsourced metalwork as well as the drive.
- [ ] Read the assembly, commissioning and stop/disconnect instructions. If a required section is incomplete, get the missing information before proceeding.

## 3. Mounting

The mount supports both the machine and the loads created by its motion. It also needs a suitable connection to the floor, furniture or other supporting structure. These are separate requirements: a strong hinge doesn't guarantee a stable base.

Think of the complete connection as:

**Supporting surface → base → adjustable mount → machine interface → machine**

[Shicks Mount Modernised][shicks] is one option. It combines 4040 extrusion, fabricated hinge plates and printed components. Its [assembly guide](shicks-mount-modernised.md) is still WIP; drilling dimensions, the updated washer stack and testing guidance need to be completed before it can be followed as a full build procedure.

Leave room for adjustment and motion, keep pinch points clear, and make sure the stop/disconnect control stays accessible. Suction cups or added weight are not suitable for every surface or setup. Check the retention method rather than assuming the base cannot move.

## 4. Controller and remote

The controller drives the motor; the remote is how you command it. Treat the board, firmware, motor configuration, remote and power supply as a compatible set. A connector that fits physically is not proof of electrical compatibility.

The Capstan parts list includes an OSSM control board and remote, with a board-only option for wireless control. **The supported wireless remote/firmware combinations are not yet listed here.** Check compatibility before buying one; don't assume any wireless implementation works with any board.

For motor-side programming, follow [AIM motor setup](aim-motor-setup.md). Its main workflow is independent of your computer's operating system; optional computer FAQs cover driver and port-access problems.

Motor programming, controller flashing and machine commissioning are separate jobs. Confirm the controller firmware, motion scaling and stopping procedure, including what happens if control or connectivity is lost.

## 5. Attachments

The end effector provides a nominal **24 mm threaded interface**. Check thread form, engagement, clearance and retention before choosing an attachment; the diameter alone doesn't guarantee a match.

The files here include a [24 mm attachment project][dp] and a [quick-change strap remix][straps]. The strap remix uses TPU. Its connection can slip under high load when lubricant reaches it, so keep that limitation in mind when choosing and inspecting the attachment.

Check the complete connection before use and follow cleaning and inspection guidance appropriate to the actual materials and components. An attachment's appearance or print thickness does not establish a load capacity. Detailed interface and material guidance is still being completed.

## 6. Accessories

| Accessory | Files and information | What to check |
| --- | --- | --- |
| Suction-cup bracket | [Model folder][suction] and [repository overview][repo] | Surface suitability, retention limitations and specified hardware |
| Weight-plate bracket | [Project README][weights] | Correct bracket/nut variant, plate fit, fixing hardware and safe handling |
| Motor cover and cooling | [Capstan parts guidance][capstan-tools] | Part of the current HG20 hardware set; the old standalone motor-cover folder has been removed |

Cooling, strain relief and safety provisions are not cosmetic extras. Check what your chosen build requires before leaving a component out.

## 7. Sourcing your parts

Decide which work you want to do yourself: printing, hardware sourcing, fabrication, assembly and electronics setup. If buying a kit, check exactly what it includes and which revision it matches. Stock, prices and shipping coverage can change, so use the seller's current information.

The [Superbuy guide][superbuy] describes an optional forwarding service, and the [JLCCNC guide][jlccnc] describes one metal-plate ordering route. Neither is required for every builder. Use a suitable supplier for your location and check dimensions, materials, quantities and revision against the BOM.

**The Capstan and Shicks parts lists still contain unresolved differences**, described in their assembly guides. Don't treat this overview as a complete shopping list or guess between conflicting quantities.

## 8. Before first operation

A complete assembly inspection and commissioning procedure for your hardware is essential. This includes mounting checks, first-power-on and homing, direction/travel limits, testing the stop/disconnect control, and maintenance requirements. These device-specific procedures are not yet complete in this guide.

Do not use a person as a load during commissioning. Keep people clear of moving machinery, know how to disconnect it, and stop if anything is unverified, loose, damaged or behaving unexpectedly. These general precautions do not replace the missing device-specific procedure.

[capstan]: ../../Capstan%20OSSM%20XL/readme.md
[capstan-tools]: ../../Capstan%20OSSM%20XL/Assembly%20Guide%20%28WIP%29/2.%20Tools%20And%20Parts.md
[shicks]: ../../Shicks%20Mount%20Modernised/readme.md
[dp]: ../../24mm%20DP%20Attachment/README.md
[straps]: ../../Quick%20Change%20Strap%20Toy%20Mount%20Remix/
[suction]: ../../Suction%20Cup%20Bracket/
[weights]: ../../Weight%20Plate%20Bracket/readme.md
[superbuy]: ../../Beginner%27s%20Guide%20to%20the%20%27Ultimate%27%20OSSM%21/Superbuy.md
[jlccnc]: ../../Beginner%27s%20Guide%20to%20the%20%27Ultimate%27%20OSSM%21/JLCCNC.md
[repo]: ../../README.md
