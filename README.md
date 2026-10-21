# USB-C 5V Input & Protection Board

Protected USB-C power input with a regulated 3.3 V rail for small embedded circuits.

This repository contains a KiCad-editable reference design intended for a junior PCB designer portfolio. It is a preliminary engineering design, not a certified or production-released product.

## Design brief

- **Difficulty:** Beginner
- **Revision:** A
- **Target board:** 2-layer FR-4, 1 oz copper, 45 x 25 mm target outline
- **Design status:** schematic and PCB source included; fabrication outputs are preliminary and require a final KiCad review.

## Main specifications

- USB-C receptacle in power-only sink configuration
- 5 V input over-voltage clamp and resettable fuse
- AP2112K-3.3 low-noise 600 mA LDO
- Power-good LED, test points, 2.54 mm output header
- 2-layer FR-4, 1 oz copper, 45 x 25 mm target outline

## Repository layout

- `usb-c-5v-protection-3v3-board.sch` — editable KiCad legacy schematic source.
- `usb-c-5v-protection-3v3-board.kicad_pcb` — editable KiCad PCB source.
- `usb-c-5v-protection-3v3-board.kicad_pro` — KiCad project metadata.
- `BOM.csv` — component list with manufacturer part numbers.
- `images/` — readable schematic and placement renders.
- `manufacturing/` — preliminary Gerber and drill set.
- `docs/` — design notes and bring-up checklist.

## Key design decisions

CC1 and CC2 are each fitted with 5.1 kOhm Rd resistors to advertise a sink. VBUS is fused before the TVS/LDO path. The board is not a USB data interface.

The layout target is two layers with a continuous ground plane on the bottom layer. Use 0.20 mm signal traces, 0.50 mm low-voltage power traces where practical, and at least 0.20 mm clearance for a standard low-cost fabrication process. Increase copper width for high-current paths after calculating temperature rise. Place connectors on board edges, keep polarity and signal names on silkscreen, and provide labeled test points.

## Verification status

KiCad was not available in the execution environment, so **ERC and DRC were not run**. No claim of ERC/DRC pass is made. Before ordering, open the project in KiCad, update symbols and footprints from the installed libraries, run ERC and DRC, resolve every warning, verify the netlist and inspect the antenna/thermal areas.

## Post-fabrication test checklist

1. Inspect solder joints, connector orientation, polarity markings and antenna keepout.
2. With no power applied, measure resistance between every supply rail and GND; investigate any low resistance before powering.
3. Power through a current-limited bench supply. Confirm input current is within the expected no-load range.
4. Measure the regulated rail before attaching the functional load.
5. Verify test points and interface signals with a DMM or oscilloscope.
6. For motor hardware, start with a current-limited supply and no mechanical load; measure bridge temperature and current during the actual duty cycle.

**Executed tests:** file generation and structural checks only. **Not executed:** KiCad ERC/DRC, electrical bring-up, RF performance, thermal validation, USB compliance, and motor-load testing.

## BOM

| Ref | Description | Value | Package | Manufacturer / MPN |
|---|---|---|---|---|
| J1 | USB-C receptacle, power-only | USB-C | USB_C_Receptacle_USB2.0_16P | GCT USB4105-xx-A |
| F1 | PTC resettable fuse 500 mA | 500mA | Fuse_1206 | Bourns MF-MSMF050-2 |
| D1 | TVS diode, 5 V standoff | SMBJ | SMBJ5.0A | Littelfuse SMBJ5.0A |
| U1 | 600 mA LDO, 3.3 V | SOT-23-5 | AP2112K-3.3 | Diodes Inc. AP2112K-3.3TRG1 |
| C1 | 10 uF input ceramic | 10uF | C_0805 | Murata GRM21BR61A106KE51 |
| C2 | 10 uF output ceramic | 10uF | C_0805 | Murata GRM21BR61A106KE51 |
| R1 | 1 kOhm LED resistor | 1k | R_0603 | Yageo RC0603FR-071KL |
| D2 | Green power LED | LED 0603 | LED_0603 | Lite-On LTST-C190KGKT |
| J2 | 3V3/GND/5V output | 1x03 2.54mm | PinHeader_1x03 | Samtec TSW-103-07-G-S |
| TP1 | 5 V test point | TH | TestPoint | Keystone 5011 |
| TP2 | 3.3 V test point | TH | TestPoint | Keystone 5011 |
| TP3 | GND test point | TH | TestPoint | Keystone 5011 |

## Primary sources

- [AP2112K regulator datasheet](https://www.diodes.com/assets/Datasheets/AP2112.pdf)
- [USB Type-C specification overview](https://usb.org/document-library/usb-type-cr-cable-and-connector-specification-release-22)
- [Littelfuse SMBJ series datasheet](https://www.littelfuse.com/assetdocs/smbj-datasheet?assetguid=6f9e6b4f-4b18-4b72-8a60-8d8d8d4f4d2d)

## Manufacturing notes

Use the supplied Gerbers only as a review artifact. The current PCB source contains a placement/routing skeleton and must be opened in KiCad for final footprint assignment, net connectivity, filled zones, design-rule setup, and verified fabrication export.
