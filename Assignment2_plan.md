# Assignment 2 Plan and Step-by-Step Guide

## Overview
This document describes a clear plan for solving Assignment 2 of the IC Design program. Assignment 2 requires:

- Layout of INVX1 and INVX2 standard cells in Magic
- DRC clean layout with height 2.72 µm for INVX1 (and similar for INVX2)
- LVS check between layout and schematic/netlist
- Parasitic extraction (PEX) from layout
- Simulation of the extracted PEX netlist with NGSpice
- Comparison of schematic and layout dynamic characteristics in a table

## Prerequisites
- Existing INVX1 and INVX2 schematics/netlists from Assignment 1
- Sky130A PDK installed in the IIC-OSIC tools environment
- Magic layout tool available
- Netgen available for LVS
- NGSpice available for simulation

## Deliverables
- Layout files for INVX1 and INVX2
- Extracted netlists from layout (`invx1_layout.spice`, `invx1_pex.spice`, `invx2_layout.spice`, `invx2_pex.spice`)
- DRC clean screenshot for INVX1 and INVX2
- LVS clean screenshot for INVX1 and INVX2
- Simulation results for schematic and PEX netlists
- Report PDF with annotated screenshots, graphs, and tables

---

## Step-by-Step Guide

### Step 1: Review Assignment 1 Designs
1. Open the INVX1 and INVX2 netlists from Assignment 1.
2. Confirm device sizes and subcircuit structure:
   - INVX1: NMOS W=0.42 µm, PMOS W=1.32 µm, L=0.15 µm
   - INVX2: a stronger inverter with larger device widths
3. Confirm the schematic topology and port naming for LVS.

### Step 2: Prepare Magic Environment
1. Launch Magic with the Sky130A PDK.
2. Create a new layout cell for INVX1.
3. Set the cell height to exactly 2.72 µm.
4. Follow the standard cell structure:
   - Place PMOS and NMOS transistors with correct spacing
   - Create VDD and VSS rails on metal1
   - Route input and output pins according to standard cell convention
5. Ensure the layout uses the PDK rules and layers for Sky130A.

### Step 3: Perform DRC in Magic
1. Run Magic DRC on the INVX1 layout.
2. Fix any reported violations until DRC reports zero errors.
3. Capture a screenshot showing the layout dimensions and DRC clean status.
4. Repeat layout and DRC for INVX2.

### Step 4: Extract the Layout Netlist
1. In Magic, extract the layout netlist after DRC clean:
   - Generate `invx1_layout.spice` for INVX1
   - Generate `invx2_layout.spice` for INVX2
2. Verify these netlists include transistor devices and interconnect nodes.
3. Compare the generated layout netlist with the original schematic netlist structure.

### Step 5: Run LVS with Netgen
1. Use Netgen to compare the layout netlist against the schematic/netlist.
2. Provide the correct subcircuit names for INVX1 and INVX2.
3. Confirm the LVS reports a clean match.
4. Capture screenshots of the clean LVS report for INVX1 and INVX2.

### Step 6: Extract the Parasitic PEX Netlist
1. In Magic, extract the parasitic netlist from the layout:
   - Generate `invx1_pex.spice`
   - Generate `invx2_pex.spice`
2. Confirm the PEX netlist contains parasitic capacitances and routing parasitics.
3. Inspect the netlist to identify added capacitor and resistor elements.

### Step 7: Simulate the PEX Netlists in NGSpice
1. Use NGSpice to simulate the extracted PEX netlist.
2. Reuse the same testbench structure from Assignment 1, adapted to the PEX netlist.
3. Extract dynamic characteristics:
   - Rise time `tr`
   - Fall time `tf`
   - Propagation delay `tp`
4. Simulate both schematic and PEX netlists so results can be compared.
5. Plot waveforms and VTC as needed.

### Step 8: Record and Compare Results
1. Build the result table for INVX1 and INVX2:
   - Rise time `tr`
   - Fall time `tf`
   - Propagation delay `tp`
2. Compare schematic vs. layout/PEX results.
3. Include observations about parasitic effects on delay.

### Step 9: Prepare the Report
1. Include the following items in the PDF report:
   - Annotated layout screenshot with height measurement
   - DRC clean screenshot
   - LVS clean screenshot
   - Table comparing schematic and layout dynamic characteristics
   - Plot screenshots or waveform screenshots
   - Explanation of layout choices and results
2. Add code snippets showing the commands used in Magic, Netgen, and NGSpice.
3. Document any issues and how they were resolved.

---

## Suggested Command Flow

### Magic
- Open cell and start layout
- Run DRC until clean
- Extract layout netlist: `extract all`
- Write netlist: `write spice invx1_layout.spice`
- Extract parasitics: `extract all` then `xtop` or `write spice invx1_pex.spice`

### Netgen
- Run LVS:
  `netgen -batch lvs invx1_layout.spice invx1_schematic.cir sky130A.tech` (example)

### NGSpice
- Simulate PEX netlist:
  `ngspice -b invx1_pex.spice`

---

## Notes for ETH Zurich IC Design Style
- Keep the layout compact and uniform.
- Use the sky130A PDK rules strictly.
- Label axes and units clearly in all plots.
- Include both schematic and layout results for each inverter.
- Provide concise observations about the impact of parasitics.

## File to Record Progress
- `Assignment2_plan.md` (this file)
- Incrementally update the file with progress notes and commands.

---

## Next Actions
1. Start by opening Magic and creating INVX1 layout.
2. Complete DRC and LVS for INVX1 first.
3. Then repeat the process for INVX2.
4. Finish with PEX simulation and report preparation.
