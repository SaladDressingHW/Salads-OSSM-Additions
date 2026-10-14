# Shicks Mount Modernised — assembly guide

[All guides](README.md) · [Capstan XL](capstan-xl-hg20.md)

> **WIP — not yet a complete assembly procedure or load-rating document.** This guide covers the mount with separate front/back TPU washers. Drilling dimensions, the updated washer stack and testing guidance are still incomplete. Do not drill, assemble an uncertain stack or load the mount based on the photos alone.

## 1. Before you start

Shicks Mount Modernised combines aluminium extrusion, metal hinge plates, printed hinge parts and adjustable clamps. It modernises Shick's double-extrusion mount and incorporates work by armpitMFG and Thomas; see the [project overview][overview] for the original designs and credits.

This guide follows the double-arm example. It does not establish a load rating or approve every extrusion profile and mounting configuration. Before ordering, choose your profile and match the parts to it. “4040” describes the overall size, not every detail inside the extrusion!

### Record your configuration

| Choice | Your build |
| --- | --- |
| Extrusion | 4040, manufacturer/profile: **fill in** |
| Printed hinge variant | Aluxprofile-specific or generic; **check actual profile fit** |
| Feet / arm lengths | Example: two 400 mm feet and three 475 mm arms; check your intended configuration |
| Hinge plates | Example: two bottom plates at 5 mm and two top plates at 3 mm |
| Lever and washer stack | **Not yet verified:** lengths, order and front/back TPU quantities |
| Machine attachment / base retention | **Fill in**; the hinge assembly alone does not provide these |

The Aluxprofile hinge variant is designed around that profile's geometry. Other manufacturers may use different slots or internal shapes, even at the same nominal size.

## 2. Parts and printing

### Purchased and fabricated parts

The [BOM][overview] and [hardware list][hardware] cover the example's 4040 extrusion, four 4080 corner brackets, metal hinge plates, clamping hardware and end caps. Base hardware and **per-hinge** hardware are listed separately; don't multiply the entire list by the hinge count.

**Some quantities and the washer stack still need confirmation.** The table is a hardware reference, not a final verified shopping list.

| Item | Listed quantity / specification | Notes |
| --- | --- | --- |
| Corner bracket fixings | 16 M8×14 ISO 7380 + 16 sliding M8 T-nuts for four brackets | Match the extrusion. The Aluxprofile example uses the linked supplier's “3030” T-nut variant. |
| Hinge plate fixings | Per hinge: 6 M8×14 ISO 7380 + 6 sliding M8 T-nuts | A diagram identifying each complete hinge and its fixings is still needed. |
| Pivot hardware | Per hinge: 1 M8×60 cap screw, 3 M8×24 washers, 1 M8×40 washer, 2 M8 nuts | From Hardware.txt; washer notation and exact stack still need confirmation. |
| Adjustable lever | M8×80, one per hinge | Listed separately from the M8×60 cap screw; both locations need identifying. |
| Metal plates | 2 × bottom, 5 mm; 2 × top, 3 mm | Use the linked STEP files, not printable substitutes. |
| End caps | 8 for the example double-arm build | Purchase or print; check the number of exposed ends in your layout. |

Use [SideHingeLasered_Bottom.step][bottom-plate] for the **5 mm bottom plate** and [SideHingeLasered_Top.step][top-plate] for the **3 mm top plate**. Their outlines differ; they are not the same plate made at two thicknesses.

Give the matching file to your fabricator. These models are **not extrusion drilling templates** and do not contain the assembled hinge or washer stack. Measured CAD dimensions are kept in the [review notes](review-notes.md#cad-reference-measurements), not presented as manufacturing tolerances.

The BOM specifies stainless steel. Confirm material, thickness, quantity and drawing revision with your fabricator; do not assume another material is equivalent. The [JLCCNC guide][jlccnc] covers one ordering option.

### Printed parts

Choose the matching files from [3D printed parts][models]. Alternatives are included; do not print the whole folder or treat its file count as a parts list.

| Part | Choose / use | Print guidance |
| --- | --- | --- |
| HingeLong_Bottom.stl or HingeLong_Bottom_Aluxprofile.stl | Bottom / 5 mm plate variant; match the extrusion | 2 HingeLong pieces per hinge, angled orientation, supports, 6 walls and 20% infill. Hinges.3mf uses Aluxprofile models. |
| HingeLong_Top.stl or HingeLong_Top_Aluxprofile.stl | Top / 3 mm plate variant; match the extrusion | Same orientation requirements. Do not swap top and bottom parts by appearance. |
| WasherBack_Bottom.stl / WasherBack_Top.stl | Match the plate thickness | 1 per hinge; angled orientation, supports recommended, at least 9 walls. |
| WasherFront.stl | Front rigid washer | 1 per hinge; print solid and verify the sliced toolpaths. |
| TPU_Washer_Back.stl | Renamed from TPU_Washer.stl | TPU, 100% infill; **quantity/stack not yet verified**. |
| TPU_Washer_Front.stl | Separate front washer | TPU, 100% infill; **quantity/stack not yet verified**. Do not replace with the back washer. |
| LeverHandle.stl | Lever-handle part | Compatible lever, material, settings and retention still need documenting. No separately named 3MF. |
| end cap.stl | Printed 4040 end cap | Profile fit and print settings still need documenting. No separately named 3MF. |

Use the angled orientations in the supplied projects. **The rear rigid washer can break when tightened if printed in the wrong orientation.** Inspect the sliced part, supports and nut-pocket layers before printing.

### Supplied 3MF projects

- **Hinges.3mf:** two bottom and two top Aluxprofile hinge objects; PLA, 0.2 mm layers, 6 walls, 20% infill.
- **Washers.3mf:** one bottom rear washer, one top rear washer and two front rigid washers. Rear objects use 9 walls. Front objects set 2 mm top/bottom shell thickness, while project infill remains 20%. **Check that the sliced front washers are actually solid.** The global infill percentage alone does not answer that.
- **TPU_Washers_Back.3mf:** four objects still internally named TPU_Washer.stl; TPU and 100% infill.
- **TPU_Washers_Front.3mf:** four front-washer objects; TPU and 100% infill.

Select profiles for **your** printer, nozzle and filament, then check supports and per-object settings in the sliced preview. The saved machine profile is not a requirement. **Plate copy counts are not verified assembly quantities**; confirm the washer count from the resolved hardware stack.

### Unresolved parts information

The older README says two TPU washers per hinge, but the newer files separate front and back washers. The complete stack and per-hinge quantities are not yet established here. The M8×80 adjustable lever and M8×60 cap screw may be separate fasteners, not conflicting alternatives; their positions still need a labelled diagram.

Steel grade/finish, permissible substitutions and the current tested configurations also need confirmation. The project's testing status remains WIP. Do not treat the photos as proof of a load capacity.

## 3. Prepare your workspace

Keep the machine disconnected and off the mount while working on the base. Support long extrusion sections so they can't fall or swing when a joint is released. Check metal edges for burrs and use suitable hand/eye protection for fabrication work.

Sort the base, bottom-hinge, top-hinge and machine-attachment hardware into separate groups. Identify the front/back TPU pieces before they are hidden inside a joint. **Get a dimensioned plan before drilling anything.**

![Extrusion, hinge plates and hardware laid out for assembly][photo-layout]

*Lay out the parts before starting. Use the parts list for quantities; overlapping pieces in a photo are easy to miss.*

- [ ] Extrusion profile and selected print variants match.
- [ ] Plate thicknesses/material and hardware have been checked.
- [ ] Prints have no cracks or damaged load-bearing features.
- [ ] The final washer/lever configuration is confirmed before assembling the joints.

## 4. Assembly — WIP

The photos below show the main subassemblies. **They do not yet form a verified step-by-step procedure.** Hidden dimensions, tightening requirements and the updated washer stack cannot be established from these views alone.

### 4.1 Extrusion and base

The build requires drilling the extrusion. [This close-up shows an access hole][photo-hole], but its diameter, location, depth and relationship to the hinge hardware are not yet specified here. **Do not scale dimensions from the photo or use its measuring tape as a drilling template.**

The base uses two feet, a lower arm and four corner brackets. Bracket fasteners/T-nuts must match the extrusion slots. Exact bracket positions, fastening order and tightening guidance still need to be documented; keep the base supported during alignment.

Inspection needs to cover squareness, rocking and whether all intended bracket fixings are seated. These checks do not replace the missing placement and drilling instructions.

### 4.2 Bottom hinge plates and inserts

**Parts:** two 5 mm bottom plates, matching bottom HingeLong pieces, extrusion and plate-fixing hardware.

![Bottom hinge plate and its row of extrusion fixings][photo-plate]

*The row of extrusion fixings is separate from the pivot and clamp hardware.*

[Side view of the paired plates][photo-side].

Match the bottom plate thickness to the bottom printed parts. Exact placement on the extrusion, component orientation, access-hole alignment and captive-nut insertion order are still incomplete. Do not force a printed part into an incompatible profile.

The assembled plates need correct pairing/alignment and fully seated inserts; a photograph alone cannot verify those details.

### 4.3 Moving arm and washer/clamp stack — not yet verified

**Do not assemble the current washer stack from these photos alone.** The front/back TPU files were split after the photos were taken. Their applicability to the updated stack still needs checking. The STEP files contain only metal plates, so they do not resolve washer order or quantity either.

![Lever and washer components laid out beside the hinge][photo-stack]

*Reference layout before the front/back TPU file split; not a verified current insertion order.*

![Adjustable lever installed alongside the hinge plate][photo-lever]

*Side view of the lever assembly. Hidden washers, thread engagement and tightening limits are not established by this view.*

A complete diagram must identify every rigid washer, TPU washer, metal washer, nut, bolt and lever, including quantity and which face points toward the plate. That diagram and the final thread-engagement/tightening requirements are not yet available here. Don't infer the stack from silhouettes.

With the arm supported, the finished joint will need checks for free adjustment when released and secure holding when clamped, without cracking, interference or an unsecured pivot. **A no-load adjustment check does not establish a load rating.**

### 4.4 Upper hinge

**Parts:** two 3 mm top plates, top HingeLong pieces, top rear washer and the confirmed remaining clamp hardware.

[Upper-hinge plate layout][photo-top-layout] · [Upper hinge with lever][photo-top-lever]

The upper hinge uses the top/thinner-plate variants. It is not simply a repeat of the bottom hinge with identical parts. Support the moving arm during adjustment.

Exact placement, assembly order, washer-stack differences and compatible arm lengths still need to be documented. Inspection must cover interference through the approved adjustment range, missing fasteners and uncontrolled arm movement.

### 4.5 Completed mount and machine attachment — WIP

![Double-arm mount with both hinge stages assembled][photo-complete]

*Overall example layout. This image does not establish a tested load capacity.*

Before adding the machine, the mount needs compatible end caps where appropriate and inspection of the complete structure. Machine/PitClamp attachment, its fasteners, base retention and a staged verification procedure are not yet fully specified here.

The [suction-cup and weight-plate accessories][repo] are separate options, not automatic approval for a particular floor, load or setup. Do not hang a machine from an unverified joint or use a person to test stability.

## 5. Adjustment, inspection and maintenance — WIP

Device-specific setup/operation guidance is still incomplete. Before powered use, the instructions need to establish:

- How to support the machine and arms before loosening a lever.
- Which joints are adjustable, their permitted range and how to relock them.
- Inspection of clamping, base retention and machine attachment.
- A staged test with stop conditions for slipping, cracking, loosening or instability.
- Inspection/replacement intervals for TPU pads and structural prints, including wear and creep.
- Clear pinch points and continued access to the machine's stop/disconnect control.

Do not proceed to powered testing without that procedure and a verified mounting configuration.

[overview]: ../../Shicks%20Mount%20Modernised/readme.md
[hardware]: ../../Shicks%20Mount%20Modernised/Hardware.txt
[models]: ../../Shicks%20Mount%20Modernised/3D%20printed%20parts/
[bottom-plate]: ../../Shicks%20Mount%20Modernised/SideHingeLasered_Bottom.step
[top-plate]: ../../Shicks%20Mount%20Modernised/SideHingeLasered_Top.step
[jlccnc]: ../../Beginner%27s%20Guide%20to%20the%20%27Ultimate%27%20OSSM%21/JLCCNC.md
[repo]: ../../README.md
[photo-layout]: ../../Shicks%20Mount%20Modernised/Assembly%20Guide%20%28WIP%29/img/IMG20260820183134.jpg
[photo-hole]: ../../Shicks%20Mount%20Modernised/Assembly%20Guide%20%28WIP%29/img/IMG20260820183632.jpg
[photo-plate]: ../../Shicks%20Mount%20Modernised/Assembly%20Guide%20%28WIP%29/img/IMG20260820183850.jpg
[photo-side]: ../../Shicks%20Mount%20Modernised/Assembly%20Guide%20%28WIP%29/img/IMG20260820184353.jpg
[photo-stack]: ../../Shicks%20Mount%20Modernised/Assembly%20Guide%20%28WIP%29/img/IMG20260821125228.jpg
[photo-lever]: ../../Shicks%20Mount%20Modernised/Assembly%20Guide%20%28WIP%29/img/IMG20260821125300.jpg
[photo-top-layout]: ../../Shicks%20Mount%20Modernised/Assembly%20Guide%20%28WIP%29/img/IMG20260821130342.jpg
[photo-top-lever]: ../../Shicks%20Mount%20Modernised/Assembly%20Guide%20%28WIP%29/img/IMG20260821130742.jpg
[photo-complete]: ../../Shicks%20Mount%20Modernised/Assembly%20Guide%20%28WIP%29/img/IMG20260821131130.jpg
