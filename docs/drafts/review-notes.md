# Documentation review checklist

Technical and editorial checks to resolve before these WIP guides can become complete assembly instructions. Keep the unresolved safety limits visible in the guides until the corresponding procedure has been verified; changing the wording does not resolve a hardware question.

## Builds covered

These guides cover HG20 with integrated strain relief, the 10/15/20 mm rail-end choices, and Shicks with separate front/back TPU washers. Keep those parts separate from the older designs. The [motor guide](aim-motor-setup.md) explains the limits of its single-motor bench test.

The older assembly STEP embeds older end parts and an extra CableCover body with no matching current STL. Do not present it as the exact current assembly without reconciling these differences. The older HGR PDF uses printed end pulleys/MR115 bearings and older fastener lengths; the MGN12H PDF covers a deprecated design.

## Editorial scope

- Keep the main guides platform-neutral: no assumed operating system, distribution, user path, serial port, adapter chip or printer profile.
- Put computer-specific drivers, permissions and commands in the separate [Windows](computer-setup-windows.md) and [Linux](computer-setup-linux.md) FAQs. Label example paths/groups; do not present them as universal settings.
- Keep the normal workflow short. Put manual Modbus procedures, tool implementation details and the single-motor record in the [motor technical reference](aim-motor-reference.md).
- Preserve verified hardware-specific requirements and unresolved safety limits. Simpler prose must not turn a bench result or CAD measurement into compatibility or commissioning approval.

### CAD reference measurements

These inspection results explain draft choices; they are not manufacturing tolerances or extrusion drilling instructions:

| Model | Measured geometry |
| --- | --- |
| Capstan drum prints | Main Ø35 × 42 mm, top Ø35 × 20 mm; nested span 44 mm, not 62 mm. No separate bushing or heat-shrink solid. |
| Shicks bottom plate | 152.000 × 150.887 × 5.000 mm envelope; three Ø8.000 mm circular fixing holes, 29.625 mm adjacent-centre / 59.250 mm first-to-last spacing. |
| Shicks top plate | 170.250 × 142.417 × 3.000 mm envelope; three Ø8.000 mm circular fixing holes, 27.000 mm adjacent-centre / 54.000 mm first-to-last spacing. |
| Older Capstan heatsink reference | Approximately 40 × 40 × 19.91 mm; not evidence of the required heat performance or attachment method. |

The plate table does not enumerate other cut-outs. Each Shicks STEP contains only a plate, not the complete hinge.

## Capstan XL

- [ ] Confirm the release/model revision this guide should cover, including the status of CableCover and the revised head/motor covers.
- [ ] Resolve the nut totals, rope purchase versus cut length, tested rope specification and cooling requirements listed in the guide's BOM comparison.
- [ ] Verify the proposed fastener assignments against every current joint, including length, insertion direction and engagement. Bore diameter is not a complete fastener specification.
- [ ] Document fit/measurement tolerances for the rail offsets. The cut-end-to-hole-centre rule has CAD/STL support, but assumes full seating against the socket stop.
- [ ] Confirm standalone pulley-cover/standoff orientations, alternative head-cover print settings, the lower-wall-count cover exceptions and material/heat requirements.
- [ ] Document the current drum glue surfaces, heat-shrink position, bushing/shaft fit and assembly method. Use adhesive-specific full-cure instructions rather than a universal 24-hour rule.
- [ ] Document motor/carriage/ring orientation, nut locations and tightening guidance.
- [ ] Document pulley/bearing/spacer stack, cover retention and running clearances.
- [ ] Supply a complete rope path: wrap direction/count for supported rail lengths, clamp engagement, tensioner travel, standoff retention and rope-trimming allowance.
- [ ] Establish a repeatable tension criterion and limits; do not replace this with “guitar string tight” or “as tight as possible”.
- [ ] Supply terminal-labelled wiring, cable lengths/gauges/terminations, board orientation, connector retention and cooling/cover installation order.
- [ ] Reconcile CAD adapter name R7B-P1J with BOM ordering code R7BF-P1J.
- [ ] Complete secure-mounting, electrical inspection, accessible stop/disconnect, first-power-on, homing/direction/travel, supervised no-load testing and maintenance procedures.

### Illustrations still needed

- Both cut rail ends with end-to-hole-centre measurements and chosen filenames.
- Current drum dry-fit order, glued surfaces/cross-section and finished rope-contact surface.
- Motor-head front/rear views with screw lengths, nut types and the current standoff identified.
- Each rail-end pulley/cover assembly with hardware and rope groove visible.
- Overall rope path with arrows, plus open/closed tensioner close-ups.
- Board/motor terminals, captured strain-relief connector and cover-interior cable/heatsink clearance.

## Motor setup and startup direction

- [ ] Define supported 57AIM30/60AIM40F revisions and controller/firmware combinations. The earlier approval to use Gold Motor settings was reported second-hand; one successful bench migration is not universal compatibility evidence.
- [ ] Preserve the distinction between motor programming and controller firmware/motion scaling.
- [ ] Resolve the motor datasheet's supply-label inconsistency for the purchased variant.
- [ ] Verify the setup/recovery instructions with another build, including power-cycle readbacks and safe stopping.
- [ ] Confirm the first physical movement at boot and publish a labelled PCB-side view before promoting the provisional direction table to instructions.

### Direction-source limitation

The source conversation described **“forward motion first”**, followed by **“in”**. The follow-up interpreted that as **“extend first”** and recorded polarity **1**, clockwise viewed from the PCB side, with the **24 mm adapter on the right** in that view.

The excerpt does not include subsequent confirmation of that interpretation or the viewing arrangement. “In” could also be read as inward/retract. The bench test recorded registers, not movement. Therefore the guide must continue to label extension-first, PCB-side clockwise and right-hand placement as **unverified** until the intended build and viewpoint are confirmed. The default 0x09 = 1 is separately supported by the linked programming source.

The needed illustration must identify which PCB is meant, the viewing direction, the shaft's clockwise direction and the adapter side. Do not equate “PCB side” with the rear motor connector by assumption. Never treat direction polarity as a reason to reverse the DC supply leads.

## Shicks Mount Modernised

- [ ] Establish the exact front/back TPU, rigid washer, metal washer, nut, bolt and lever order/count per hinge and per mount. 3MF plate copy counts are not a BOM.
- [ ] Identify the M8×80 adjustable lever and M8×60 cap screw locations; they may be separate fasteners rather than contradictory lengths.
- [ ] Verify whether front-washer toolpaths are solid with the 3MF's 20% project infill and 2 mm shell overrides; correct the source if they are not.
- [ ] Specify compatible lever/handle retention, optional parts, end-cap fit and print settings.
- [ ] Confirm steel grade/finish and permissible substitutions. The plate STEP files confirm 5/3 mm thicknesses, but contain no complete hinge assembly.
- [ ] Supply extrusion hole diameter, named reference face/end, position, through-depth, tools and deburring guidance. Plate fixing-hole spacing is not an extrusion drilling template.
- [ ] Document bracket/plate placement, captive-nut insertion, alignment, fastening order and tightening guidance.
- [ ] Document differences between the lower and upper hinge, permissible arm lengths and adjustment ranges.
- [ ] Verify the current washer revision against each reused photo; the photos predate the separate front/back TPU file names.
- [ ] Supply machine/PitClamp attachment, base retention, staged tests/stop conditions and inspection/replacement criteria for prints and TPU.
- [ ] Confirm the actually tested configurations before changing the WIP/testing status or adding load claims.

### Illustrations still needed

- Dimensioned extrusion drilling and bracket/plate placement drawings.
- Current washer/clamp stack laid out in insertion order, with every part and facing surface labelled.
- Assembled joint from both sides, showing engagement and the differences between top and bottom hinges.
- Machine-to-mount attachment, base retention and adjustment/pinch-point views.

## Beginner guide and navigation

- [ ] Complete the mounting/interface compatibility overview and a labelled system diagram.
- [ ] Document supported wired/wireless remote and firmware combinations, including loss-of-control behaviour and stop/disconnect access.
- [ ] Specify attachment thread/interface compatibility, retention, material-specific cleaning and inspection guidance.
- [ ] Resolve BOM discrepancies before publishing a consolidated beginner shopping list.
- [ ] Review the original introduction's body/scale force test; do not carry it into the new guide as validated selection guidance. A person must not be the commissioning load.
- [ ] Integrate approved text into the existing chapter locations instead of maintaining two competing manuals.
- [ ] Turn the original beginner overview into working chapter links.
- [ ] Fix Shicks' nonexistent Assembly.md link and the removed standalone motor-cover image/folder link in the root README.
- [ ] Fix the Capstan /../Hardware/ link, obsolete beginner-folder URLs in sourcing tables and the empty Shicks link in the JLCCNC guide.
- [ ] Correct old part labels: TensionerBottom.stl / TensionerTop.stl have no underscore; the motor-cap picture is not MotorHead_Front.stl.
- [ ] Resolve the old end-effector “0.8 mm” finer-layer suggestion. The supplied projects use 0.12 mm; do not silently assume 0.08 mm was intended.

## Final review

- [ ] Every complete assembly step has the required parts, an action, a useful illustration and an inspection check.
- [ ] No unsupported torque, drilling, wiring, load or motion claims have become instructions through editing alone.
- [ ] Main guides remain platform-neutral; OS-specific commands are confined to the computer FAQs and use clearly labelled examples.
- [ ] Technical sources and all local links/anchors resolve.
- [ ] A builder can follow the guide without extra verbal instructions.
- [ ] Credits to the original designers remain intact.
- [ ] Remove obsolete review material once each issue has been resolved in the actual guides.
