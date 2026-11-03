# Case for RP-Voyager

The plan is to make a case from wood with CNC, optionally with FDM 3D printer.

## Thickness stackup (bottom to top)

- 3mm bottom solid wood (bottomWidth)
- 3mm clearance for PCB surface-mounted components (pcbBottomClearance)
- 1.6mm thick PCB (standard FR4; pcbWidth)
- 0.2mm thick lip for the Mill-Max 0305-2-15 (to be added to plateLevel)
- top clearance for keyswitches (to be added to plateLevel)
  - Gateron KS-33: 2.5mm - 1.2mm plate = 1.3mm
  - Kailh Choc: 2.2mm - 1.2mm plate = 1.0mm
- 1.2mm Top plate (plateWidth)

plateWidth:

- width Kailh Choc: 2.4mm
- with Gateron KS-33: 2.7mm

Overall case thickness:

- with Kailh Chock: 10mm
- with Gateron KS-33: 10.3mm

Make changes to `plateWidth` in [rp-voyager.FCStd](mechanical/rp-voyager.FCStd) in VarSet to generate the appropriate case.

## Design input

While the overall layout is coming from the FreeCAD design (see "realestate" sketch), the ultimate guide from the plate is coming from the PCB 3D model exported from KiCad. It is placed as `mechanical/board_v1.2.step`. All the exports are imported to the FreeCAD model.

## Design output

The FreeCAD design is in `mechanical/rp-voyager.FCStd` file. It defines the following bodies:

- tray: planned left part of the keyboard case, with glued-up posts for plate fixture and PCB support
- plate: 1.2 mm thick plate with switch cutouts
- plate-right-v1: right-side plate for pre-1.2 PCB design, where switch positions were slightly off
- tray-with-stands: same as tray, but posts for the plate and PCB support are added for single 3D print
- reset: tiny device for pressing the reset button

The design also contains all released versions of the PCB board render from KiCad.
