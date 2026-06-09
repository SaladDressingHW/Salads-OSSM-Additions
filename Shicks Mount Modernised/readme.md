# Shick's Mount Modernised
This is a modernisation, remix and compilation of the original Shick's Double Extrusion Mount as well as some mods done by [armpitMFG](https://github.com/armpitMFG). In addition to that, this is a centralized documentation for a heavy duty friendly mount, where even the biggest toys at long levers aren't able to make the mount slip. 

This is a WIP that is also still in testing, which is on hold due to lack of funds. Since it is just a reiteration (mostly making things bigger and stronger) of proven designs however, I am confident it will work nicely. I also have one more trick up my sleeve should the current strength still not suffice.

The Parts compiled and remixed here are the following:
|                  Part                  | Link                                                                           | Modification(s) done                                               |
|:--------------------------------------:|--------------------------------------------------------------------------------|--------------------------------------------------------------------|
| Original Double Extrusion Shicks mount | not hosted anywhere anymore, afaik                                             | Just using the hinge long part + f3d files                         |
|       300° Hinge Plate by armpit       | [Discord](https://discord.com/channels/559409652425687041/1214771415430078525) | Holes realligned, changed thickness                                |
|      Lever Clamp System by armpit      | [Discord](https://discord.com/channels/559409652425687041/1209004178421055598) | Reworked from the ground up to make it much bigger and more stable |
|       Metal Hinge by Thomas & Me       | [Discord](https://discord.com/channels/559409652425687041/1445780533991833810) | New Part                                                           |

# BOM
This BOM has heavy duty use in mind. Feel free to downscale for less demanding setups. More info in my beginners OSSM guide (releasing soon).
|                                                        Part                                                       | Amount                                         | Link                                                                          |
|:-----------------------------------------------------------------------------------------------------------------:|------------------------------------------------|-------------------------------------------------------------------------------|
| 4040 Extrusion I recommend aluxprofile for people in Europe, Hinge is optimized for it (it's what I have on hand) | I use 2 x 400 mm for feet, 3 x 475 mm for arms | https://www.aluxprofil.de/aluminium-nutprofil-4040/a3619?m=4259               |
|                                          4040 end caps, or print your own                                         | 8 for double arm                               | e.g. https://www.aluxprofil.de/profilabdeckkappe-4040/a3528                   |
|                                4080 corner brackets, best for heavy duty stability                                | 4                                              | https://de.aliexpress.com/item/1005009745995530.html                          |
|                                               M8x80 adjustable lever                                              | 1 per hinge                                    | https://de.aliexpress.com/item/1005008368566274.html                          |
|                                          Laser Cut Hinge Plates, stainless steel                                         | 2 bottom (5mm) + 2 top (3mm)                               | "SideHingeLasered" files, order at your favorite laser cut shop, I use JLCCNC <br> [How to order from JLCCNC]() |
|                                                      Hardware                                                     | see Hardware.txt                               | see Hardware.txt                                                              |

You will also need something to drill through the aluminium extrusion. A hand drill with according metal drill bit should suffice.

# Printing
**HingeLong**: You need 2 of these per Hinge. For 5mm hinge plates you will need the "Bottom" one, and for 3mm hinge plates the "Top" one. print them at an angle for best stability, see my .3mf. .3mf is for the Aluxprofile version as that is what I have. F3d file is attached so you can modify it to fit your own 4040 profile. Supports are needed. 6 Walls, 20% infill suffices.

**WasherBack**: Print one per hinge, again "Top" and "Bottom" versions depending on your plate thickness. Also needs to be printed at an angle, or it **will** break when tightening a lot. Again, see .3mf for orientation. Supports recommended. Print at 9 Walls or more to properly support the nut.

**WasherFront**: One is need per hinge. Print it 100% solid.

**TPU_Washer**: 2 per hinge are needed. Print it 100% solid. Out of TPU, as the name implies. I recommend printing TPU by Object for the least stringing. Especially if you haven't dried your Tpu like me.

# Assembly Guide
[Link](Assembly.md) (WIP)