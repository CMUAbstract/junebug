# Notes for KiCad

* Install the correct version.

```bash
sudo add-apt-repository ppa:js-reynaud/kicad-5.1
sudo apt update
sudo apt install kicad
```

* Open KiCad and choose `File > New > Project...`. Select the project location.
  Un-check "Create a new directory for the project," and type the project name
  (here: `junebug`).

* Launch `Eeschema` (Schematic Layout Editor). Accept "Copy default global
  symbol library table (recommended)." Choose `File > Page Settings...` and
  select "Size: USLetter 8.5x11in"

* Next, open the Symbol Editor by choosing `Tools > Symbol Library Editor` from
  `eeschema`.

* Using the Symbol Editor, choose `File > New Library...`. Enter the project
  name (here: `junebug`), and choose the "Project" scope when prompted.

* Import the BOM symbols provided by `componentsearchengine.com` (free account
  required). Select `File > Import Symbol...` and save in the project library.
  The `.lib` files are provided in the `components/` directory.

* Open the Footprint Editor. Accept "Copy default global footprint library table
  (recommended)." Choose `File > New Library...`. Enter the project name
  (here: `junebug`), and choose the "Project" scope when prompted.

* Open the Footprint Editor and build three custom footprints:
  `MountingHoles_Feather`, `PinSocket_1x16_Feather`, and `PinSocket_6x2_DCMI`.
  See below for details on each custom footprint. Save each footprint in the
  project library. Choose `File > New Footprint...` to get started.

**Feather Mounting Holes**

* Size (x): 3 mm
* Hole size (x): 2.54 mm
* Locations: 1 (-22.86,-8.89), 2 (22.86,-8.89), 3 (-22.86,8.89), 4 (22.86,8.89)
* Labels locations: (0,-12), (0,12)

**Feather Pin Sockets**

* Size (x): 1.54 mm
* Hole size (x): 1 mm
* Locations: 1 (-19.05,0.00), 2 (-16.51,0.00), 3 (-13.97,0.00), 4 (-11.43,0.00),
  5 (-8.89,0.00), 6 (-6.35,0.00), 7 (-3.81,0.00), 8 (-1.27,0.00), 9 (1.27,0.00),
  10 (3.81,0.00), 11 (6.35,0.00), 12 (8.89,0.00), 13 (11.43,0.00),
  14 (13.97,0.00), 15 (16.51,0.00), 16 (19.05,0.00)
* Labels locations: (0,-3), (0,3)

**DCMI Pin Sockets**

* Size (x): 1.54 mm
* Hole size (x): 1 mm
* Locations: 1 (-1.27,-6.35), 2 (1.27,-6.35), 3 (-1.27,-3.81), 4 (1.27,-3.81),
  5 (-1.27,-1.27), 6 (1.27,-1.27), 7 (-1.27,1.27), 8 (1.27,1.27),
  9 (-1.27,3.81), 10 (1.27,3.81), 11 (-1.27,6.35), 12 (1.27,6.35)
* Labels locations: (0,-12), (0,12)

* Import the BOM footprints from `componentsearchengine.com` into the project
  footprint library. Select `File > Import Footprint from KiCad File...` and
  save in the project library. The `.kicad_mod` files are provided in the
  `footprints/` directory.

* Lay out the schematic in `eeschema`. Set the appropriate label values.

* From `eeschema`, select `Tools > Annotate Schematic...` and choose "Use the
  entire schematic;" "Keep existing annotations;" "Sort components by X
  position;" and "Use first free number after 0."

* Also from `eeschema`, choose `Tools > Assign Footprints...` and set the
  footprints.

* Specify footprints that cannot be set automatically:
  `629105150521 : Connector_USB:USB_Micro-B_Wuerth_629105150521`,
  `Conn_01x16 : junebug:PinSocket_1x16_Feather`, and
  `599-0040-007F : junebug:LEDM168X70N`

* Open `pcbnew` (PCB Layout Editor) and choose `File > Page Settings...` to
  select "Size: USLetter 8.5x11in"

* Add the PCB outline with graphic lines and graphic arcs.

**Graphic Lines for PCB Edge**

* (76,78.54) to (76,96.32)
* (78.54,76) to (124.26,76)
* (78.54,98.86) to (124.26,98.86)
* (126.8,78.54) to (126.8,96.32)

**Graphic Arcs for PCB Edge**

Create the following in the Edge.Cuts layer:
* (78.54,78.54) to (78.54,76) with arc angle -90.0
* (124.26,78.54) to (126.8,78.54) with arc angle -90.0
* (78.54,96.32) to (76,96.32) with arc angle -90.0
* (124.26,96.32) to (124.26,98.86) with arc angle -90.0

* Add `MountingHoles_Feather` at (101.4,87.43) and `PinSocket_6x2_DCMI` at
  (124.26,87.43)

* From `eeschema`, choose `Tools > Generate Netlist File...` and select
  "Generate Netlist."

* From `pcbnew`, choose `Tools > Load Netlist...` and browse to the appropriate
  file.

* Place the components, vias, and tracks. The Feather Pin Sockets are placed at
  (101.40,77.10,0.0) and (101.40,97.76,0.0). Other components:
  * J1: (79.50,87.43,-90.0)
  * LEDR1: (79.00,81.50,180.0)
  * LEDY1: (79.00,93.36,180.0)
  * R1: (82.00,80.70,90.0)
  * R2: (82.00,94.16,-90.0)
  * IC4: (85.50,80.80,180.0)
  * IC3: (90.50,80.90,0.0)
  * C1: (84.40,84.90,-90.0)
  * C2: (86.90,84.90,-90.0)
  * C3: (89.40,84.90,-90.0)
  * C4: (91.90,84.90,-90.0)
  * C5: (88.05,91.45,180.0)
  * C6: (96.50,79.80,0.0)
  * C7: (102.50,79.80,0.0)
  * C8: (105.50,79.80,0.0)
  * C9: (102.50,95.20,180.0)
  * C10: (105.50,95.20,180.0)
  * R3: (96.50,95.20,180.0)
  * IC1: (100.00,87.43,180.0)
  * IC2: (111.80,82.00,0.0)
  * Y1: (109.60,87.70,90.0)
  * Y2: (109.40,93.00,90.0)
  * C11: (114.20,86.30,0.0)
  * C12: (114.20,88.80,0.0)
  * C13: (114.20,91.30,0.0)
  * C14: (114.20,93.60,0.0)
  * S1: (119.30,82.80,90.0)
  * S2: (119.30,91.50,90.0)

* Via positions:
  * LEDR: (78.3,81.5)
  * LEDY: (78.3,93.36)
  * Net-(IC1-Pad43): (82.8,89.3)
  * Net-(IC1-Pad45): (83.2,88.4)
  * Net-(IC1-Pad44): (83.6,87.5)
  * EN: (84.5,79.7)
  * LEDR: (85.7,85.2)
  * LEDY: (85.7,87.4)
  * NRST: (86.35,95.8)
  * SWCLK: (87.5,88.2)
  * SWCLK: (87.5,93.7)
  * SWDIO: (88.6,88.2)
  * SWDIO: (88.6,91.2)
  * EN: (89.3,79.7)
  * GND: (89.3,80.9)
  * GND: (89.3,86.3)
  * VUSB: (90.7,84.6)
  * VBAT: (90.7,92.9)
  * NRST: (91.2,95.8)
  * VDD: (91.9,79.7)
  * VDD: (91.9,83.5)
  * GND: (91.9,86.3)
  * VUSB: (92.8,88.2)
  * Net-(IC1-Pad44): (92.8,89.7)
  * SWDIO: (92.8,91.2)
  * 13: (93.8,81.6)
  * VDD: (94.1,92)
  * 12: (94.8,81.6)
  * 13: (95.4,84.2)
  * Net-(IC1-Pad43): (95.4,88.7)
  * Net-(IC1-Pad45): (95.4,89.7)
  * GND: (95.4,90.7)
  * SWCLK: (95.7,93.7)
  * GND: (95.7,95)
  * VDD: (95.8,79.7)
  * 12: (96,83.6)
  * A0: (96,84.8)
  * NRST: (96.3,96.6)
  * A1: (96.6,84.2)
  * GND: (97.2,79.7)
  * 6: (97.2,87.6)
  * MSCK: (97.7,83)
  * 11: (97.9,88.1)
  * MCE: (98.3,79.4)
  * VBAT: (98.4,90.2)
  * 10: (98.6,88.6)
  * MIO0: (98.7,83)
  * A5: (99.3,89.2)
  * A2: (99.3,90.2)
  * SCK: (99.2,94.3)
  * MIO1: (99.8,80.2)
  * A4: (100.2,89.2)
  * A3: (100.2,90.2)
  * MOSI: (100.3,94.3)
  * 4: (100.5,87.6)
  * MIO3: (100.7,80.2)
  * MIO2: (100.9,83)
  * MISO: (101.1,91.9)
  * RX: (101.3,87.2)
  * TX: (102.1,86.8)
  * NRST: (102.2,90.4)
  * TX: (102.38,83)
  * GND: (103.2,79.7)
  * VDD: (103.2,95.1)
  * NRST: (103.4,91.3)
  * A1: (104.6,84.2)
  * SDA: (104.5,87.4)
  * VDD: (104.8,79.7)
  * BOOT: (105,93)
  * TX: (105.8,83)
  * A0: (107.1,84.8)
  * SCL: (107.1,86.3)
  * 5: (107.1,90.9)
  * VDD: (107.2,95.1)
  * MCE: (108.2,79.9)
  * MIO1: (108.2,81.4)
  * MIO2: (108.2,82.9)
  * 6: (110.5,83.9)
  * 11: (111.4,79.9)
  * 11: (111.4,83.9)
  * 10: (112.3,79.9)
  * 10: (112.3,83.9)
  * 5: (113.2,83.9)
  * BOOT: (113.3,96)
  * 4: (114.1,96.6)
  * MIO3: (115.3,81.4)
  * MSCK: (115.3,82.6)
  * MIO0: (115.3,83.9)

* `pcbnew`: `Preferences > Preferences...` Pcbnew Units: Inches

* `pcbnew`: `File > Board Setup...`
  * Design Rules: Prohibit overlapping courtyards
    * Minimum track width: 6.0 mils
    * Minimum via diameter: 20.0 mils
    * Minimum via drill: 10.0 mils
    * Minimum uVia diameter: 20.0 mils
    * Minimum uVia drill: 10.0 mils
    * Minimum hole to hole: 8.0 mils
  * Net Classes (Edit the Default)
    * Clearance: 6.0 mils
    * Track Width: 6.0 mils
    * Via Size: 27.0 mils
    * Via Drill: 13.0 mils
    * uVia Size: 27.0 mils
    * uVia Drill: 13.0 mils
    * dPair Width: 6.0 mils
    * dPair Gap: 6.0 mils
  * Solder Mask/Paste
    * Solder mask clearance: 2.0 mils
    * Solder mask minimum width: 4.0 mils

* `pcbnew`: `Preferences > Preferences...` Pcbnew Units: Millimeters

* `pcbnew`: `Edit > Edit Track & Via Properties...` Set to net class values OK

* Perform design rules check

* Add the text to F.SilkS and B.SilkS: Width 0.4, Height 0.4, Thickness 0.1
* Pin labels (all 0.0 degrees)
  * SWCLK: (82.35,78.4)
  * SWDIO: (84.9,78.4)
  * GND: (87.4,78.4)
  * VIN: (90.0,78.4)
  * VCAP: (92.5,78.4)
  * EN: (95.1,78.4)
  * VUSB: (97.6,78.4)
  * 13: (100.1,78.4)
  * 12: (102.7,78.4)
  * 11: (105.2,78.4)
  * 10: (107.8,78.4)
  * 9: (110.3,78.4)
  * 6: (112.8,78.4)
  * 5: (115.4,78.4)
  * SCL: (117.9,78.4)
  * SDA: (120.5,78.4)
  * NRST: (82.35,96.46)
  * 3V3: (84.9,96.46)
  * AREF: (87.4,96.46)
  * GND: (90.0,96.46)
  * A0: (92.5,96.46)
  * A1: (95.1,96.46)
  * A2: (97.6,96.46)
  * A3: (100.1,96.46)
  * A4: (102.7,96.46)
  * A5: (105.2,96.46)
  * SCK: (107.8,96.46)
  * MOSI: (110.3,96.46)
  * MISO: (112.8,96.46)
  * RX: (115.4,96.46)
  * TX: (117.9,96.46)
  * 4: (120.5,96.46)
* Part labels:
  * LEDR: (76.8,81.5,90.0)
  * LEDY: (76.8,93.36,90.0)
  * J1: (78.8,87.43,0.0)
  * R1: (80.8,79.9,90.0)
  * R2: (80.8,94.46,90.0)
  * C1: (84.4,84.6,0.0)
  * IC4: (85.5,79.4,0.0)
  * C2: (86.9,84.6,0.0)
  * C5: (88.05,91.45,0.0)
  * C3: (89.4,84.6,0.0)
  * IC3: (91.75,80.9,0.0)
  * C4: (91.9,84.6,0.0)
  * C6: (94.8,79.8,90.0)
  * R3: (94.8,95.2,90.0)
  * IC1: (100.0,87.43,0.0)
  * C7: (100.8,79.8,90.0)
  * C9: (100.8,95.2,90.0)
  * C8: (105.5,81.0,0.0)
  * C10: (105.5,94.0.0.0)
  * Y2: (109.4,93.0,0.0)
  * Y1: (109.6,87.6,0.0)
  * IC2: (111.8,82.0,0.0)
  * C11: (113.8,86.3,90.0)
  * C12: (113.8,88.8,90.0)
  * C13: (113.8,91.3,90.0)
  * C14: (113.8,93.6,90.0)
  * S1: (119.3,82.8,0.0)
  * S2: (119.3,91.5,0.0)

* Add logo information (try `http://img2mod.wayneandlayne.com`)

* Export the Gerber and Drill files
  (see `https://docs.oshpark.com/design-tools/kicad/generating-kicad-gerbers/`)
  * Select `File > Plot...` and provide an output directory
  * Choose the following layers: `F.Cu`, `B.Cu`, `F.SilkS`, `B.SilkS`, `F.Mask`,
    `B.Mask`, and `Edge.Cuts`; also `F.Paste` and `B.Paste`
  * Check "Exclude PCB Edge from other layers;" check "Use Protel filename
    extensions"
  * Select `Plot`
  * Select `Generate Drill File`
  * Check "Decimal Format;" uncheck "Mirror Y Axis;" check "Merge PTH and NPTH
    Holes into one file"
  * Select `Drill File`

## License

Copyright 2019 Bradley Denby

Licensed under the Apache License, Version 2.0 (the "License"); you may not use
this file except in compliance with the License. You may obtain a copy of the
License at <http://www.apache.org/licenses/LICENSE-2.0>.

Unless required by applicable law or agreed to in writing, software distributed
under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
CONDITIONS OF ANY KIND, either express or implied. See the License for the
specific language governing permissions and limitations under the License.
