# Build guides

Welcome! Whether you're planning your first OSSM build or updating an existing one, start here. These guides cover the Capstan OSSM XL, Shicks Mount Modernised, motor setup and the parts that connect everything together.

> **Work in progress.** The assembly and commissioning instructions are not complete yet. Sections marked **WIP** or **not yet verified** are not ready to build from. Read the whole guide before ordering parts, and don't guess at missing wiring, drilling or setup details.

## Where to start

| Guide | What it covers |
| --- | --- |
| [Beginner's guide](beginners-guide.md) | Choosing a drive, mount, controller and attachments; planning the complete build |
| [Capstan OSSM XL — HG20](capstan-xl-hg20.md) | Choosing the correct printed parts, rail-end offsets, print settings and assembly preparation |
| [Shicks Mount Modernised](shicks-mount-modernised.md) | Extrusion and plate choices, printed hinge parts and assembly reference photos |
| [AIM motor setup](aim-motor-setup.md) | Safe RS485 connection, Gold Motor settings and returning from OSSM-rs |

If you're new to the project, start with the beginner's guide. Already have your parts? Check the hardware revision and variant choices in the relevant assembly guide before printing or putting anything together.

## Optional troubleshooting and technical detail

The main guides do not assume a particular operating system, USB adapter, port name or printer. Start with the normal workflow; use these pages only when you need them:

| Reference | When to use it |
| --- | --- |
| [Windows computer setup FAQ](computer-setup-windows.md) | USB adapter drivers, COM-port selection or browser access problems |
| [Linux computer setup FAQ](computer-setup-linux.md) | USB detection, serial permissions or browser access problems |
| [AIM motor technical reference](aim-motor-reference.md) | Manual Modbus diagnosis, advanced baud restoration or the single-motor bench record |

Other operating systems may work with a supported browser and adapter. Check their documentation rather than applying another system's commands. These computer FAQs do not change motor wiring or electrical requirements.

## Pick the right parts

These guides cover the HG20 build with integrated strain relief, the 10/15/20 mm rail-end options, and the separate front/back TPU washers for Shicks. Start with the parts for your build—there's no need to print the whole folder!

- Use the **top-level HG20 parts** for the current Capstan build. The MGN12H version is deprecated; the no-strain-relief motor head is in a separate legacy folder.
- Use the supplied **3MF projects as references for orientation and part-specific settings**. Select your own printer/nozzle/filament profiles and inspect the sliced result. An STL's saved orientation is not necessarily its printing orientation.
- Choose alternatives deliberately. Downloading every STL does not mean you need to print every file.
- Do not mix the older PDF assembly steps with the current hardware. Pulley designs, fasteners and motor-head parts have changed.

## A quick note about the CAD files

The main assembly STEP is older than some of the individual parts, so don't treat it as an exact shopping list. CAD dimensions help identify parts; they do not establish a load rating, electrical compatibility or a tested assembly. Motor programming is also separate from machine commissioning: matching register values does not prove that direction, homing or travel limits are correct.

For the original OSSM hardware and community, see [KinkyMakers/OSSM-hardware](https://github.com/KinkyMakers/OSSM-hardware) and the [KinkyMakers Discord](https://discord.gg/NcueGt87u).
