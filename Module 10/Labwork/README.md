# Lab: Power Distribution Network (PDN) Construction

## Contents

1. Lab: Steps to Build the Power Distribution Network
2. Lab: From Power Straps to Standard-Cell Power Rails
3. Key Takeaways

---

## 1. Lab: Steps to Build the Power Distribution Network

### Objective

To understand how OpenLane constructs the Power Distribution Network (PDN) for a SKY130 design using OpenROAD. The process includes creating power rings, power straps, standard-cell power rails, and connections between different metal layers.

### 1.1 Introduction to PDN

A Power Distribution Network distributes the supply voltage and ground connections throughout the chip.

- **VDD:** Positive power supply.
- **VSS:** Ground supply.
- **Core Power Ring:** A ring surrounding the core that distributes power and ground.
- **Power Straps:** Wider metal wires that distribute power across the core.
- **Standard-Cell Power Rails:** Horizontal or vertical supply rails connected to the power pins of standard cells.
- **Vias:** Connections between metal layers that allow power to move from one layer to another.

The PDN diagram shows the core ring surrounding the design, power straps crossing the core, standard-cell power connections, and a separate power ring around the RAM macro.

### 1.2 Understanding the OpenLane Environment

The lab uses the OpenLane flow with the SKY130 PDK and the `picorv32a` design.

OpenLane automatically generates the PDN during the floorplanning stage using its configured power-grid scripts.

**Step 1: Navigate to the OpenLane directory.**

```bash
cd ~/Desktop/work/tools/openlane_working_dir/openlane
```

**Step 2: Launch the interactive OpenLane flow.**

```bash
./flow.tcl -interactive
```

**Step 3: Prepare the design.**

At the OpenLane Tcl prompt, execute:

```tcl
prep -design picorv32a
```

This prepares the design, loads the configuration, and creates a run directory for the current execution.

The run directory contains the intermediate files, generated layouts, reports, and logs.

**Step 4: Perform logic synthesis.**

```tcl
run_synthesis
```

Logic synthesis converts the RTL design into a gate-level netlist using the selected standard-cell library.

**Step 5: Run floorplanning.**

```tcl
run_floorplan
```

During this stage, OpenLane performs the required floorplanning operations, including I/O placement, tap and decap cell placement, and PDN generation.

The power-grid generator creates the configured power and ground structures and writes the resulting design database and DEF files.

**Note:** In the normal OpenLane flow, the PDN is generated automatically during `run_floorplan`. The manual OpenROAD Tcl commands described in Section 2 are an alternative for understanding or constructing a PDN separately; they should not be run again on a design that already contains the same PDN.

### 1.3 Configuring the Power Distribution Network

The power-grid configuration determines the structure and dimensions of the PDN.

Important configuration variables include:

| Variable | Purpose |
|---|---|
| `DESIGN_IS_CORE` | Identifies whether the design is treated as a core. |
| `FP_PDN_CORE_RING` | Enables the core power ring when supported by the selected configuration. |
| `FP_PDN_VPITCH` | Controls the pitch of the configured vertical power straps. |
| `FP_PDN_VOFFSET` | Controls the offset of the configured vertical power straps. |
| `FP_PDN_HPITCH` | Controls the pitch of the configured horizontal power straps. |
| `FP_PDN_HOFFSET` | Controls the offset of the configured horizontal power straps. |

The following are example settings corresponding to the values shown in the lab screenshots. They should be used only when appropriate for the selected PDK and existing design configuration.

```tcl
set ::env(DESIGN_IS_CORE) 1
set ::env(FP_PDN_CORE_RING) 1

set ::env(FP_PDN_VPITCH) 153.600
set ::env(FP_PDN_VOFFSET) 16.320

set ::env(FP_PDN_HPITCH) 153.180
set ::env(FP_PDN_HOFFSET) 16.650
```

These values control strap placement; they do not independently define every PDN dimension. Ring dimensions, strap widths, layer connections, and other settings are determined by the complete PDN configuration.

### 1.4 Observing PDN Generation

During the PDN-generation stage, the terminal displays information about the technology layers, vias, standard-cell rails, straps, and connections.

The screenshots show the following configuration:

| Structure | Metal layer | Width (µm) | Pitch (µm) | Offset (µm) |
|---|---|---:|---:|---:|
| Standard-cell rails | `met1` | 0.480 | 2.720 | 0.000 |
| Power straps | `met4` | 1.600 | 153.600 | 16.320 |
| Power straps | `met5` | 1.600 | 153.180 | 16.650 |

The reported layer connections are:

- `met1` to `met4`
- `met4` to `met5`

These values are taken from the supplied terminal output. They are not universal SKY130 requirements and may differ with the PDK, configuration, and OpenLane version.

### 1.5 Checking the Generated Files

After the floorplanning stage, inspect the current run directory.

On the host terminal, navigate to the OpenLane directory and list the available runs:

```bash
cd ~/Desktop/work/tools/openlane_working_dir/openlane

ls -lt designs/picorv32a/runs/
```

Locate the directory created by the latest run. Its name may contain a timestamp or a user-defined tag.

Inspect the generated results:

```bash
find designs/picorv32a/runs -path "*/results/floorplan/*" -type f
```

Inspect the PDN-related log messages:

```bash
grep -RniE "PDN|power|rail|strap|ring|via" \
    designs/picorv32a/runs/<run-directory>/logs/floorplan/
```

Replace `<run-directory>` with the actual run-directory name.

The generated floorplan DEF and log files provide information about the physical placement and the power distribution structures.

### 1.6 Expected Result

After successful PDN generation, the design should contain the configured power distribution structures:

1. A core power ring surrounding the core, if enabled.
2. Power straps distributed across the core on the selected metal layers.
3. Standard-cell power rails aligned with the standard-cell rows.
4. Connections between the rails, straps, and ring through the required metal-layer connections and vias.
5. Macro power structures where enabled and configured.

---

## 2. Lab: From Power Straps to Standard-Cell Power Rails

### Objective

To understand how power is distributed from the core ring through the higher metal layers and finally to the standard-cell power rails.

### 2.1 Understanding the PDN Structure

The PDN consists of multiple interconnected structures.

#### 1. Core Power Ring

The power ring surrounds the core and provides a distribution path for VDD and VSS.

It connects to the wider power distribution network and can connect to power pads in a complete chip design.

#### 2. Power Straps

Power straps are wider metal wires distributed across the core.

They carry supply current through the layout and provide connections to the lower-level power rails.

Different metal layers may be used to form the power grid. In the supplied screenshots, the straps use `met4` and `met5`.

#### 3. Standard-Cell Power Rails

Standard cells are arranged in rows. Their power pins must connect to the supply rails provided by the PDN.

In the supplied terminal output, the standard-cell rails are generated on `met1` with:

- Width: `0.480 µm`
- Pitch: `2.720 µm`
- Offset: `0.000 µm`

The `-followpins` option instructs the PDN generator to create rails following the standard-cell row structure.

#### 4. Vias and Layer Connections

Vias provide electrical connections between metal layers.

For the network shown in the screenshots:

`Standard-cell rails (met1) → Power straps (met4) → Power straps (met5)`

The two required layer connections are:

`met1 ↔ met4`

`met4 ↔ met5`

Together, these structures distribute the supply voltage throughout the core.

### 2.2 Manual PDN Construction Using OpenROAD Tcl

The following commands demonstrate how a PDN can be constructed manually. Use this procedure as a separate OpenROAD workflow, not as an additional execution on top of the PDN already generated by OpenLane.

The input DEF must represent the design **before the PDN is generated**. Do not use a DEF that already contains the same power grid, since this can cause duplicate or conflicting structures.

#### Step 1: Load the Technology and Design Files

Start OpenROAD in the relevant environment, with the SKY130 PDK files and the prepared design files available.

The paths below are examples; use the actual paths in your run directory.

```tcl
# Read the SKY130 technology LEF.
read_lef /path/to/sky130_fd_sc_hd.tlef

# Read the merged standard-cell LEF generated by OpenLane.
read_lef /path/to/merged_unpadded.lef

# Read the design DEF from before PDN generation.
read_def /path/to/design_before_pdn.def
```

The LEF files provide technology and cell geometry information. The DEF file provides the design's physical placement and connectivity information.

#### Step 2: Connect the Standard-Cell Power Pins to VDD and VSS

Standard-cell libraries commonly use `VPWR` and `VGND` as the main power and ground pin names. Body-bias pins may also be present.

```tcl
# Connect standard-cell power pins to VDD.
add_global_connection -net VDD -pin_pattern {^VPWR$} -power
add_global_connection -net VDD -pin_pattern {^VPB$} -power

# Connect standard-cell ground pins to VSS.
add_global_connection -net VSS -pin_pattern {^VGND$} -ground
add_global_connection -net VSS -pin_pattern {^VNB$} -ground

# Apply the global connections.
global_connect
```

The correct pin names and supply-net names depend on the selected standard-cell library and design configuration. They must match the library rather than being copied blindly.

#### Step 3: Define the Core Voltage Domain

```tcl
set_voltage_domain -name CORE -power VDD -ground VSS
```

This establishes the power and ground nets for the core voltage domain.

#### Step 4: Define the PDN Grid

```tcl
define_pdn_grid -name core_grid -voltage_domains {CORE}
```

The grid specifies the network on which the power rings, straps, rails, and layer connections will be constructed.

#### Step 5: Create the Core Power Ring

The following is an illustrative command using example dimensions. The ring width, spacing, and offsets must be selected to satisfy the actual design geometry and foundry rules.

```tcl
add_pdn_ring -grid core_grid \
    -layers {met4 met5} \
    -widths {2.0 2.0} \
    -spacings {1.0 1.0} \
    -core_offsets {4.0 4.0 4.0 4.0}
```

The ring uses two metal layers to form the surrounding power and ground structure. The exact dimensions should match the design's PDN configuration.

#### Step 6: Generate the Standard-Cell Power Rails

```tcl
add_pdn_stripe -grid core_grid \
    -layer met1 \
    -width 0.480 \
    -pitch 2.720 \
    -offset 0.000 \
    -followpins
```

The `-followpins` option creates standard-cell rails aligned with the standard-cell rows.

#### Step 7: Add the Power Straps

Add the configured power straps on `met4` and `met5`.

```tcl
add_pdn_stripe -grid core_grid \
    -layer met4 \
    -width 1.600 \
    -pitch 153.600 \
    -offset 16.320

add_pdn_stripe -grid core_grid \
    -layer met5 \
    -width 1.600 \
    -pitch 153.180 \
    -offset 16.650
```

The pitch controls the spacing between repeating strap locations, while the offset determines their placement relative to the grid origin.

The values above reproduce the strap parameters shown in the supplied log. Before using them in a different design, confirm that they match its configuration and physical constraints.

#### Step 8: Define the Connections Between Metal Layers

```tcl
# Connect the standard-cell rails to the higher metal grid.
add_pdn_connect -grid core_grid -layers {met1 met4}

# Connect the two higher metal layers.
add_pdn_connect -grid core_grid -layers {met4 met5}
```

These commands define where the PDN generator can insert the required inter-layer connections.

#### Step 9: Generate the Power Distribution Network

```tcl
pdngen
```

The PDN generator constructs the configured power and ground geometry, including rails, straps, rings, and vias where required by the grid definition.

#### Step 10: Save the Result

```tcl
write_def pdn_complete.def
```

The resulting DEF file contains the generated physical design and power-grid information.

The exact commands and supported options may vary between OpenROAD versions. Consult the documentation for the version installed in the OpenLane environment.

### 2.3 Inspecting and Verifying the PDN

After generation, inspect the terminal output and the generated DEF.

On the host terminal, replace `<run-directory>` with the actual run directory:

```bash
# List the generated floorplan results.
find designs/picorv32a/runs/<run-directory>/results/floorplan \
    -maxdepth 1 -type f

# Search the generated DEF for power-net and special-net information.
grep -nE "SPECIALNETS|VDD|VSS" \
    designs/picorv32a/runs/<run-directory>/results/floorplan/picorv32a.floorplan.def
```

Check the following:

1. The power and ground structures are present.
2. The configured metal layers have been used.
3. Standard-cell power rails have been generated.
4. The intended metal-layer connections have been created.
5. The core ring and macro power structures are present when enabled.
6. The PDN-generation logs do not report unresolved generation errors.

For a complete sign-off, use the checks supported by the installed tool flow and PDK. Generating the PDN successfully does not by itself prove that the entire design is free of all connectivity or manufacturing violations.

### 2.4 Understanding the Final PDN Diagram

The supplied diagram illustrates the following physical components:

- **Standard Cell Row:** The row in which standard cells are arranged.
- **Standard Cell Power Connections:** Connections between standard-cell supply pins and the power rails.
- **Power Stripe:** A wider metal conductor that distributes VDD or VSS across the core.
- **Core Power Ring:** The ring surrounding the core.
- **Macro Cell (RAM):** A larger embedded block that may require its own power-grid structure.
- **Block Power Ring:** A ring that distributes power around a macro.
- **Block Halo:** A reserved region around a macro used to manage placement and routing clearance.
- **I/O and Corner Pads:** Pads placed around the chip's perimeter in a pad-based design.
- **Power Pad Connections:** Connections that deliver external power into the on-chip distribution network.

The exact structures depend on whether the design is a standalone core, a macro, or a complete chip with an I/O pad frame.

### 2.5 Overall PDN Construction Sequence

`Load Design → Connect Power Pins → Define Voltage Domain → Define PDN Grid → Create Power Ring → Add Power Straps → Generate Standard-Cell Rails → Connect Metal Layers → Run PDN Generation → Inspect Results`

---

## 3. Key Takeaways

- A Power Distribution Network delivers VDD and VSS to the standard cells and macros of an integrated circuit.
- The core power ring surrounds the core and distributes power around the design.
- Power straps carry supply current through wider metal conductors on the selected metal layers.
- Standard-cell rails connect the supply pins of cells arranged in standard-cell rows.
- Vias provide the electrical connections required between different metal layers.
- In the supplied SKY130 example, the standard-cell rails use `met1`, while the wider straps use `met4` and `met5`.
- The PDN-generation log reports rail and strap dimensions, pitches, offsets, and layer connections.
- OpenLane normally generates the configured PDN automatically during `run_floorplan`.
- The `add_global_connection` commands map standard-cell power pins to the VDD and VSS nets.
- `set_voltage_domain` defines the supply and ground nets used by the grid.
- `define_pdn_grid` establishes the grid, while `add_pdn_ring`, `add_pdn_stripe`, and `add_pdn_connect` define its physical structures.
- `pdngen` generates the configured PDN, and `write_def` saves the design.
- Successful PDN generation should be followed by inspection and the appropriate connectivity, DRC, and physical-design checks.

