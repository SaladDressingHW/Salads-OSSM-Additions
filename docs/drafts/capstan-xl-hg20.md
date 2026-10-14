# Capstan OSSM XL — HG20 assembly guide

[All guides](README.md) · [Beginner's guide](beginners-guide.md)

> **WIP — not yet a complete build or operating procedure.** This guide covers the HG20 build with integrated strain relief. Mechanical assembly, wiring and commissioning details are still being checked. Stop at incomplete sections; do not power a machine on the strength of this guide alone.

## 1. Before you start

So you've decided to build a Capstan OSSM XL, or you're checking what's involved! This guide covers the **HG20 rail / HGH20HA carriage** version with a 60AIM40F motor. The deprecated MGN12H version, abandoned proof of concept and legacy motor head without strain relief are different builds.

There are five main jobs: choose your parts, print and inspect them, prepare the drum and electronics, assemble the mechanism, and commission it on a secure mount. Mounting and control are separate parts of the system; an assembled drive alone isn't ready for use.

For more background, see the [project overview][overview] and [parts guidance][tools]. Performance figures describe the mechanism, not safe force limits for a person.

### Record your build before ordering

| Choice | Your build |
| --- | --- |
| Rail and carriage | HG20 + HGH20HA; rail length: **fill in** |
| Rail end-hole offsets | End-effector end: **fill in**; rear end: **fill in** |
| Motor | 60AIM40F, +485 single-turn version; confirm the exact purchased variant |
| Control board and firmware | **Not yet specified here:** board revision, firmware release and flashing/configuration procedure |
| Motor-head cover | Standard, no-RJ45 or no-logo version; match your connector and control setup |
| Power supply and strain relief | Mean Well GST220A36-R7B + R7BF-P1J adapter; verify exact connector fit |
| Mount | **Fill in**; check compatibility separately |

The [overview][overview] documents testing with a **450 mm rail**. It lists 500/550 mm as untested possibilities, not validated alternatives. A 500 mm rail model in the STEP assembly does not change that testing status.

## 2. Choose your printed parts

Use the [current HG20 folder][models]. Don't mix in parts from the legacy no-strain-relief folder simply because the names look familiar. The [legacy note][legacy-note] recommends the integrated-strain-relief version with the specified supply.

The table below helps you choose the correct files; **it is not a final verified print-quantity BOM**. The older STEP assembly includes one current-style standoff, but also older component revisions and an extra cable-cover body that needs clarification.

| Assembly | Current STL filenames | Selection / printing project |
| --- | --- | --- |
| Drum | CapstanDrum_Main.stl, CapstanDrum_Top.stl | Both parts; CapstanDrum.3mf |
| Motor head | MotorHead_Back.stl, MotorHead_Front.stl, Standoff.stl | Current strain-relief set; back/front each have a 3MF. The STEP assembly contains **one** matching standoff body; its installation details are still being checked. Do not substitute the three legacy files. |
| Head cover | MotorHead_Cover.stl, MotorHead_Cover_noRJ45.stl, MotorHead_Cover_nologo.stl | Choose one compatible cover. MotorHead_Cover.3mf contains the standard cover; the alternatives have no separately named 3MFs. |
| Motor cover | MotorCover_Main.stl, MotorCover_Cap.stl | Both in MotorCover.3mf; check cooling/heatsink and cable clearance. |
| Motor mounting ring | Pitclamp_MotorRing_60AIM40F.stl | Matching 3MF; check compatibility with your mount and cover. |
| End effector | EndEffector_10mm.stl, EndEffector_15mm.stl, EndEffector_20mm.stl | Choose one for that rail end; each has a corresponding 3MF. |
| End-effector pulley cover | EndEffector_PulleyCover.stl | Different from the rear cover; no separately named 3MF. |
| Rear rail end | RailEnd_10mm.stl, RailEnd_15mm.stl, RailEnd_20mm.stl | Choose one for that rail end; each has a corresponding 3MF. |
| Rear pulley cover | RailEnd_PulleyCover.stl | Do not exchange with the end-effector cover; no separately named 3MF. |
| Tensioner | TensionerBottom.stl, TensionerTop.stl | Both in Tensioner.3mf. There is no underscore before Top/Bottom in the filenames. |

The folder includes alternative parts. Print the selected parts for your build, not every STL.

### Choosing a rail-end offset

With the rail **fully seated against the internal socket stop**, the filename suffix is the distance **along the rail from its cut end to the mounting-hole centre**. This matches the socket geometry and hole positions in the STEP and STL files.

Measure both rail ends separately and choose the matching 10, 15 or 20 mm part for each end. Don't measure from the outside edge of the printed part. If neither measurement matches an available variant, stop and ask about a suitable part rather than forcing it or improvising a hole. **Fit/measurement tolerances and an annotated rail photograph are not yet provided.**

Use the filename and mounting-hole position to identify a variant; overall size alone cannot distinguish the choices. The standalone STEP files do not include every offset.

### Printing and inspection

1. Open the matching 3MF **as a project**. Check orientation, supports and per-object settings. STL export orientation is not a printing instruction.
2. Select profiles for **your** printer, nozzle and filament. Do not copy the project's saved machine profile unless it matches your equipment.
3. Preview the layers around nut traps, bridging, threads and supported surfaces before printing.
4. Remove supports and inspect for cracks, delamination, blocked passages and damaged threads. Don't force an ill-fitting structural part into place.

The general [print guidance][tools] is a 0.4 mm nozzle, at least six walls and 20% infill, using the supplied orientations. Some projects have part-specific settings:

| Project(s) | Project-level settings | Notes |
| --- | --- | --- |
| Drum, motor-head back/front, ring, tensioner | PLA; 0.2 mm layers; 6 walls; 20% infill | Check per-object and support overrides too. |
| Motor cover, motor-head cover | PLA; 0.2 mm layers; 4 walls; 20% infill | Lower wall-count exceptions need checking against the chosen material and part. |
| All three end-effectors and all three rail ends | PLA; 0.12 mm layers; 6 walls; 20% infill | The older prose's “0.8 mm” finer-layer suggestion is inconsistent. Do not use that value. |

**WIP:** orientations/settings for the standalone pulley covers, standoff and alternative head covers, plus final material/heat requirements, still need confirmation. Profile metadata alone does not prove a print is strong enough.

## 3. Parts and tools

Start with the [parts list][tools], [sourcing page][hardware] and [fastener list][fasteners]. **They currently disagree on some items. Resolve those differences before ordering; don't treat either list as final.**

The main components are the motor, controller and remote, HG20 rail/HGH20HA carriage, two 6 × 29.3 × 8 mm U-groove pulleys (ID × OD × width), a 20 × 24 × 40 mm bushing, rope, epoxy, heat-shrink tubing, cables, heatsink and power supply/adapter.

### Unresolved BOM differences

| Item | Tools/parts guide | Other source | What remains unresolved |
| --- | --- | --- | --- |
| M5 / M6 nuts | 9 M5 + 2 M6 | Hardware_HG20.txt: 11 M5, no M6 entry | Final nut totals for the current pulley hardware |
| Rope purchase length | 10 m | Hardware sourcing page: 5 m | Purchase allowance versus cut length for each supported rail |
| Rope grade / diameter | DM20/SK99/SK78, around 1 mm; discusses 1.1–1.3 mm | Overview: DM20/SK99/SK75, max 1 mm | One tested specification; both sources name Liros DC Pro 161 as standard. Do not assume substitutes are equivalent. |
| Motor cooling | 40 × 40 × 20 mm heatsink | No heatsink row on the sourcing page | Requirement, attachment method and cover compatibility |

The CAD has **6.30 mm pulley-axis bores** and separate **5.40 mm rail-attachment bores**, consistent with the parts guide's M6/M5 distinction. Those dimensions do not establish nut totals or suitable screw lengths.

The M5×65 count is not necessarily a conflict: the text file lists four plus another four under “Motor Cover”, matching the guide's total of eight.

**Don't use the old PDF as the current assembly recipe.** [Assembly Guide HGR.pdf][old-pdf] uses printed pulleys/MR115 bearings instead of the current purchased U-groove pulleys. It also lists M4×12 clamp screws, M5×75 cover screws and an M5×25 drum screw, where the current guide lists M4×16, M5×80 and M5×30 respectively. Every changed joint needs checking.

### Tools

Prepare a driver, 2.5/3/4 mm hex bits, a 2 mm slotted bit, pliers, a lint-free cloth, gloves and a heat source. You'll also need suitable measuring tools for the rail offsets. Cable-termination tools depend on the verified wiring procedure, which is still incomplete.

Follow the adhesive/chemical manufacturers' PPE, ventilation and curing guidance. Keep heat sources away from flammable cleaning products.

## 4. Preparation

### 4.1 Inspect your parts

Lay everything out by subassembly: drum, motor head, rail ends, tensioner, electronics and covers. Keep alternative and legacy parts separate. Compare the motor and board labels with your build configuration before making connections.

- [ ] Correct model variants and hardware revision identified.
- [ ] Prints inspected, with no damaged load-bearing features.
- [ ] Fastener lengths and nut sizes checked against a resolved BOM.
- [ ] Rail/carriage handling and lubrication instructions available from the supplier. Keep the carriage's transport guide and avoid losing bearing balls.

### 4.2 Prepare the drum — WIP

The drum uses two nested printed parts plus the specified bushing and heat-shrink. The STEP model contains the prints, not a complete physical drum assembly; do not infer the assembly order or fit from it alone.

The older HGR guide describes a metal bushing with heat-shrink on its outside, assembled to the prints using epoxy. **The current glue surfaces, shrink-tube position, shaft orientation and fit have not yet been documented well enough to follow here.** Don't assume every old detail still applies.

Use the actual adhesive manufacturer's mixing and full-cure requirements; the old guide's fixed “24 h” is not universal. The completed drum will need checks for movement between bonded parts, a clean/undamaged rope surface, and shaft fit without forcing. Those checks do not replace the missing assembly details.

### 4.3 Configure the motor and controller — WIP

For **isolated motor-side bench setup**, follow [AIM motor setup](aim-motor-setup.md). It covers safe connection, reading/backing up settings, approved Gold Motor defaults and returning from OSSM-rs. Computer-specific troubleshooting and the advanced single-motor test record are separate optional references, not assumptions about your setup.

The complete controller revision, firmware release, motion scaling and wiring integration still need to be specified. A terminal-labelled wiring diagram must show connector orientation, supply polarity and cable termination/strain relief. Do not infer pinouts from wire colours or an STL.

**Matching motor register values does not make the assembled machine ready to energise.** First-power-on and homing remain separate, incomplete procedures.

## 5. Mechanical assembly — WIP

The sections below identify the subassemblies and hardware assignments currently listed in the parts guide. **They are not a verified assembly sequence.** Installation diagrams, orientations and tightening guidance still need to be completed before these steps can be followed as a build procedure.

### 5.1 Motor head, motor and carriage

**Parts:** current MotorHead_Back, motor, HGH20HA carriage and selected ring/cover hardware.

The parts guide assigns two M5×45 countersunk and two M5×65 cap screws to the rear-head/motor connection, and four M5×20 cap screws to the carriage. Coupling-nut locations must be distinguished from ordinary nut pockets.

**Not yet documented:** carriage/motor-terminal orientation, ring requirement, fastener insertion directions and tightening guidance. The assembly needs inspection for seated fasteners, cracked nut traps and obstructions in the carriage path or cable passages.

### 5.2 Rail ends and U-groove pulleys

**Parts:** chosen end effector and rear rail end, two purchased pulleys and their distinct printed covers.

The parts guide assigns one M5×30 screw/M5 nut to each rail-end attachment and one M6×25 countersunk screw/M6 nut to each pulley. Check the rail offsets and resolve the conflicting nut totals first. The old printed-pulley/MR115 procedure does not apply here.

**Not yet documented:** pulley orientation, bearing support/spacer stack, cover retention and clearance after tightening. Both rail ends must be positively retained, and the pulleys must turn freely without cover rubbing; these checks alone do not establish a correct hardware stack.

### 5.3 Drum, rope path and tensioner — routing not yet verified

**Parts:** cured drum, specified rope, TensionerBottom, TensionerTop, motor-head front and current standoff.

The parts guide assigns M5×30 to shaft retention, four M4×16 button-head screws/four M4 nuts to the rope clamp, and a fully threaded M5×110 screw/M5 nut to tension adjustment. The STEP assembly contains one standoff, but no rope-routing model.

**Do not route or tension the rope from this description alone.** Wrap count/direction, clamp engagement, shaft-screw installation, standoff retention, adjustment travel and trimming allowances still need a complete diagram and procedure. The old PDF's “guitar string tight” wording does not define a repeatable setting or safe upper limit.

Checks will need to cover non-crossing wraps, sharp edges/rubbing, reserve adjustment travel and free movement through the intended range with power disconnected. Don't guess a tension or use a powered run to discover a routing error.

### 5.4 Wiring, strain relief, cooling and covers — WIP

**Parts:** verified controller/cables, selected head cover, motor-cover main/cap, heatsink, supply connector/adapter and specified fasteners.

Use the current parts list and validated wiring diagram, not the older assembly STEP, to choose electronics and covers. That STEP includes older cover revisions and **CableCover**, which has no matching current STL. Reference board models do not establish pinouts or firmware.

**Not yet resolved:** whether CableCover is required, the CAD adapter name versus the BOM's R7BF-P1J ordering code, heatsink attachment and complete cable/cover clearances. Board model names do not establish firmware or pinouts.

The parts guide assigns two M3×12 screws/M3 nuts to board mounting, four M5×80 countersunk screws to the head cover, and four M5×65 cap screws with M5×20 coupling nuts to the motor cover. These assignments still need checking against the final wiring and assembly order.

Use a validated wiring diagram and the exact connector the strain relief supports. Cable gauges/lengths, terminations, board orientation, connector retention and cover installation are not yet fully documented. Work only with power disconnected; obtain qualified help if you cannot verify the electrical work.

## 6. Inspection and commissioning — WIP

**The complete first-power-on and operating procedures are not ready yet.** Do not treat the list below as permission to operate.

Direction polarity **1** is the documented motor-setting default, not proof of homing direction. The [motor guide](aim-motor-setup.md#startup-direction-and-orientation) lists the provisional extension-first, PCB-side clockwise and right-hand-adapter arrangement, clearly marked as unverified. It must be confirmed before relying on it; direction polarity is not DC supply polarity.

The commissioning procedure still needs to define:

- Secure mounting and inspection of every load-bearing joint.
- Electrical/polarity and cable-retention checks before applying power.
- A verified, immediately accessible stop/disconnect method and its test procedure.
- First-power-on, homing, direction and travel-limit checks with people clear and nothing attached for use.
- A staged, supervised no-load test with approved settings and explicit stop conditions.
- Repeatable rope inspection/retensioning criteria, not “as tight as possible”.
- Maintenance intervals and rejection criteria for rope, prints, pulleys, wiring and rail components.

Never use a person as a load test. Keep hands, clothing and loose cables away from the rope, pulleys and rail whenever motion is possible.

[overview]: ../../Capstan%20OSSM%20XL/readme.md
[tools]: ../../Capstan%20OSSM%20XL/Assembly%20Guide%20%28WIP%29/2.%20Tools%20And%20Parts.md
[models]: ../../Capstan%20OSSM%20XL/Hardware/3D%20printed%20parts/HG20/
[legacy-note]: ../../Capstan%20OSSM%20XL/Hardware/3D%20printed%20parts/HG20/%5Blegacy%5D%20No%20Strain%20Relief/readme.md
[hardware]: ../../Capstan%20OSSM%20XL/Hardware/README.md
[fasteners]: ../../Capstan%20OSSM%20XL/Hardware/Hardware_HG20.txt
[old-pdf]: ../../Capstan%20OSSM%20XL/Assembly%20Guide%20HGR.pdf
