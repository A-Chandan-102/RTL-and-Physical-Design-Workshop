# RTL Design and Physical Design Workshop

Welcome to my RTL Design and Physical Design Workshop repository, where I document my journey of learning RTL coding, simulation, testbench development, waveform-based debugging, logic synthesis, and full RTL-to-GDSII physical implementation of digital circuits. All the data is ordered according to modules learnt.

> ✅ **Course status: Completed.** All 10 modules, 5 classworks and the assessment are documented in this repository.

## 🎯 Main Objective

The goal of this workshop is to build a solid, hands-on understanding of the complete **RTL-to-GDSII front-end and back-end flow**:

- **RTL Design (Modules 1–5, Classwork 1–5, Assessment 1):** writing and simulating Verilog RTL designs, moving through logic synthesis and standard-cell mapping using the open-source **SKY130 PDK**, and validating designs through **Gate-Level Simulation (GLS)**. Along the way, the focus is on understanding coding-style pitfalls (blocking vs non-blocking assignments, incomplete if/case constructs), synthesis optimizations (constant propagation, cloning, retiming), and how RTL design choices translate into real synthesized hardware.
- **Physical Design (Modules 6–10):** taking a synthesized netlist through the **OpenLane** RTL-to-GDSII flow — floorplanning, power planning, placement, and standard-cell design — plus the fundamentals of **CMOS fabrication**, SPICE-based **CMOS inverter characterization**, custom standard-cell layout in **Magic**, LEF/timing-library generation, and pre-layout timing analysis and clock-tree concepts. The flow is completed with **detailed routing** (Lee's algorithm, global vs detailed routing, **TritonRoute**), **Design Rule Checks (DRC)**, **parasitic extraction**, and **Power Distribution Network (PDN)** construction.

## 🗺️ Modules at a Glance

| Module | Topic | Key ideas |
| ------ | ----- | --------- |
| **Module 1** | Introduction, Icarus Verilog, GTKWave and Yosys | Tool setup, simulation, first synthesis |
| **Module 2** | Timing libraries, hierarchical vs flat synthesis, flip-flops | Liberty file, PVT corners, reset styles |
| **Module 3** | Combinational and sequential optimisation | Constant propagation, cloning, retiming, unused outputs |
| **Module 4** | Gate-Level Simulation and mismatches | Blocking vs non-blocking, sensitivity lists |
| **Module 5** | If, case and loop constructs | Latch inference, complete vs incomplete statements |
| **Module 6** | Introduction to SoC design and OpenLane | Software to hardware, OpenLane flow |
| **Module 7** | Floorplanning, placement and cell design flow | Core/die, power planning, timing characterisation |
| **Module 8** | CMOS inverter, fabrication and tech-file labs | SPICE, Magic, SKY130 DRC rules |
| **Module 9** | Custom cell integration into OpenLane | LEF, tracks and grids, delay tables |
| **Module 10** | Detailed routing, DRC and TritonRoute | Lee's algorithm, route guides, DRC clean, parasitics, PDN |

## 🛠️ Tools Used

| Tool                            | Purpose                                                                         |
| ------------------------------- | ------------------------------------------------------------------------------- |
| **Icarus Verilog (iverilog)**   | RTL simulation / compiling Verilog testbenches                                  |
| **GTKWave**                     | Viewing simulation waveforms                                                    |
| **Yosys**                       | Logic synthesis and standard-cell mapping                                       |
| **SKY130 PDK**                  | Open-source standard-cell library used for synthesis and physical design        |
| **Graphviz / Yosys Dot Viewer** | Visualizing synthesized netlists                                                |
| **OpenLane**                    | Automated RTL-to-GDSII physical design flow (floorplanning, placement, routing) |
| **OpenROAD / TritonRoute**      | Detailed routing and PDN generation within the OpenLane flow                    |
| **Magic**                       | VLSI layout editor — custom standard-cell layout, LEF generation, DRC           |
| **ngspice**                     | SPICE simulation for CMOS inverter and standard-cell characterization           |
| **KLayout**                     | Viewing and inspecting chip layouts                                             |
| **GVim**                        | Editing RTL, testbench, and script source files                                 |
| **Git & GitHub**                | Version control and documentation                                               |

## 📂 Repository Structure

*#NOTE: Each folder below contains its own README.md with detailed notes and screenshots for that topic.*

This repository is organized into two parts:

- **Part 1 – RTL Design:** `Assesment 1`, `Classwork 1`–`5`, and `Module 1`–`5`
- **Part 2 – Physical Design:** `Module 6`–`10`

## Part 1 – RTL Design 🧩

*(`Assesment 1`, `Classwork 1`–`5`, `Module 1`–`5`)*

- 📁 **[Assesment 1/](Assesment%201/)**
  - 📄 [Assesment_abc.png](Assesment%201/Assesment_abc.png)
  - 📄 [Assesment_gates used.png](Assesment%201/Assesment_gates%20used.png)
  - 📄 [Assesment_output_waveform.png](Assesment%201/Assesment_output_waveform.png)
  - 📄 [Assesment_stat.png](Assesment%201/Assesment_stat.png)
  - 📄 [Assesments_gls.png](Assesment%201/Assesments_gls.png)
  - 📄 [Assesments_netlist.png](Assesment%201/Assesments_netlist.png)
  - 📄 [README.md](Assesment%201/README.md)
- 📁 **[Classwork 1/](Classwork%201/)**
  - 📄 [basic commands.jpeg](Classwork%201/basic%20commands.jpeg)
  - 📄 [cloned repository.jpeg](Classwork%201/cloned%20repository.jpeg)
  - 📄 [Codespaces.jpeg](Classwork%201/Codespaces.jpeg)
  - 📄 [github repository.jpeg](Classwork%201/github%20repository.jpeg)
  - 📄 [gtkwave.jpeg](Classwork%201/gtkwave.jpeg)
  - 📄 [KLayout.jpeg](Classwork%201/KLayout.jpeg)
  - 📄 [README.md](Classwork%201/README.md)
  - 📄 [terminal.jpeg](Classwork%201/terminal.jpeg)
- 📁 **[Classwork 2 & 3/](Classwork%202%20%26%203/)**
  - 📄 [latch layout diagram.jpeg](Classwork%202%20%26%203/latch%20layout%20diagram.jpeg)
  - 📄 [Mux_error.jpeg](Classwork%202%20%26%203/Mux_error.jpeg)
  - 📄 [presynth_sim.png](Classwork%202%20%26%203/presynth_sim.png)
  - 📄 [README.md](Classwork%202%20%26%203/README.md)
  - 📄 [RV_to_DAC.png](Classwork%202%20%26%203/RV_to_DAC.png)
  - 📄 [Source files.jpeg](Classwork%202%20%26%203/Source%20files.jpeg)
- 📁 **[Classwork 4 & 5/](Classwork%204%20%26%205/)**
  - 📄 [BABYSOC.jpeg](Classwork%204%20%26%205/BABYSOC.jpeg)
  - 📄 [BABYSOC2.jpeg.png](Classwork%204%20%26%205/BABYSOC2.jpeg.png)
  - 📄 [babysoc_LAYOUT.png](Classwork%204%20%26%205/babysoc_LAYOUT.png)
  - 📄 [cells in good mux.png](Classwork%204%20%26%205/cells%20in%20good%20mux.png)
  - 📄 [Comparision of good_mux with and without synthesis.png](Classwork%204%20%26%205/Comparision%20of%20good_mux%20with%20and%20without%20synthesis.png)
  - 📄 [goodmux_layout.png](Classwork%204%20%26%205/goodmux_layout.png)
  - 📄 [Post_Synth_babysoc.png](Classwork%204%20%26%205/Post_Synth_babysoc.png)
  - 📄 [presynth_babysoc.png](Classwork%204%20%26%205/presynth_babysoc.png)
  - 📄 [README.md](Classwork%204%20%26%205/README.md)
- 📁 **[Module 1/](Module%201/)**
  - 📁 **[1Introduction/](Module%201/1Introduction/)**
    - 📄 [iverilog flowchart.png](Module%201/1Introduction/iverilog%20flowchart.png)
    - 📄 [README.md](Module%201/1Introduction/README.md)
    - 📄 [testbench flowchat.png](Module%201/1Introduction/testbench%20flowchat.png)
  - 📁 **[Introduction to Yosys and Logic synthesis/](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/)**
    - 📄 [fast vs slow.png](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/fast%20vs%20slow.png)
    - 📄 [flavours of gate.png](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/flavours%20of%20gate.png)
    - 📄 [lib.png](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/lib.png)
    - 📄 [README.md](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/README.md)
    - 📄 [RTL desing.png](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/RTL%20desing.png)
    - 📄 [Synthesis illustration.png](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/Synthesis%20illustration.png)
    - 📄 [Synthesis.png](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/Synthesis.png)
    - 📄 [Synthesizer flowchart.png](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/Synthesizer%20flowchart.png)
    - 📄 [Verify synthesis.png](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/Verify%20synthesis.png)
    - 📄 [Yosys flowchart.png](Module%201/Introduction%20to%20Yosys%20and%20Logic%20synthesis/Yosys%20flowchart.png)
  - 📁 **[Lab1 - Environment Setup/](Module%201/Lab1%20-%20Environment%20Setup/)**
    - 📄 [git instalation.png](Module%201/Lab1%20-%20Environment%20Setup/git%20instalation.png)
    - 📄 [gtkwave install.png](Module%201/Lab1%20-%20Environment%20Setup/gtkwave%20install.png)
    - 📄 [gvim installation.png](Module%201/Lab1%20-%20Environment%20Setup/gvim%20installation.png)
    - 📄 [iverilog installation.png](Module%201/Lab1%20-%20Environment%20Setup/iverilog%20installation.png)
    - 📄 [README.md](Module%201/Lab1%20-%20Environment%20Setup/README.md)
  - 📁 **[Lab2 - Icarus Verilog, GTKWave and Gvim/](Module%201/Lab2%20-%20Icarus%20Verilog%2C%20GTKWave%20and%20Gvim/)**
    - 📄 [good mux code.png](Module%201/Lab2%20-%20Icarus%20Verilog%2C%20GTKWave%20and%20Gvim/good%20mux%20code.png)
    - 📄 [good_mux waveform.png](Module%201/Lab2%20-%20Icarus%20Verilog%2C%20GTKWave%20and%20Gvim/good_mux%20waveform.png)
    - 📄 [README.md](Module%201/Lab2%20-%20Icarus%20Verilog%2C%20GTKWave%20and%20Gvim/README.md)
  - 📁 **[Lab3 - Using Yosys/](Module%201/Lab3%20-%20Using%20Yosys/)**
    - 📄 [README.md](Module%201/Lab3%20-%20Using%20Yosys/README.md)
    - 📄 [Screenshot 2026-08-08 232323osys netlist.png](Module%201/Lab3%20-%20Using%20Yosys/Screenshot%202026-08-08%20232323osys%20netlist.png)
    - 📄 [Yosis dot viewer.png](Module%201/Lab3%20-%20Using%20Yosys/Yosis%20dot%20viewer.png)
    - 📄 [yosis.png](Module%201/Lab3%20-%20Using%20Yosys/yosis.png)
    - 📄 [yosys netlist.png](Module%201/Lab3%20-%20Using%20Yosys/yosys%20netlist.png)
    - 📄 [yosys vs gvim.png](Module%201/Lab3%20-%20Using%20Yosys/yosys%20vs%20gvim.png)
    - 📄 [yosys2.png](Module%201/Lab3%20-%20Using%20Yosys/yosys2.png)
    - 📄 [yosys3.png](Module%201/Lab3%20-%20Using%20Yosys/yosys3.png)
- 📁 **[Module 2/](Module%202/)**
  - 📁 **[Flip Flop coding styles/](Module%202/Flip%20Flop%20coding%20styles/)**
    - 📄 [asynchronous code.png](Module%202/Flip%20Flop%20coding%20styles/asynchronous%20code.png)
    - 📄 [asynchronous reset.png](Module%202/Flip%20Flop%20coding%20styles/asynchronous%20reset.png)
    - 📄 [Mix of sync and async.png](Module%202/Flip%20Flop%20coding%20styles/Mix%20of%20sync%20and%20async.png)
    - 📄 [README.md](Module%202/Flip%20Flop%20coding%20styles/README.md)
    - 📄 [synchronous.png](Module%202/Flip%20Flop%20coding%20styles/synchronous.png)
    - 📄 [why flops are used.png](Module%202/Flip%20Flop%20coding%20styles/why%20flops%20are%20used.png)
  - 📁 **[Lab4 - Library walkthrough/](Module%202/Lab4%20-%20Library%20walkthrough/)**
    - 📄 [and power.png](Module%202/Lab4%20-%20Library%20walkthrough/and%20power.png)
    - 📄 [comparision.png](Module%202/Lab4%20-%20Library%20walkthrough/comparision.png)
    - 📄 [differnet flavours of and.png](Module%202/Lab4%20-%20Library%20walkthrough/differnet%20flavours%20of%20and.png)
    - 📄 [Exploration of lib.png](Module%202/Lab4%20-%20Library%20walkthrough/Exploration%20of%20lib.png)
    - 📄 [PVT.png](Module%202/Lab4%20-%20Library%20walkthrough/PVT.png)
    - 📄 [README.md](Module%202/Lab4%20-%20Library%20walkthrough/README.md)
    - 📄 [Starting of cell.png](Module%202/Lab4%20-%20Library%20walkthrough/Starting%20of%20cell.png)
  - 📁 **[Lab5 -  Hier and flat synth/](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/)**
    - 📄 [cmos nand.png](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/cmos%20nand.png)
    - 📄 [direct instanteation.png](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/direct%20instanteation.png)
    - 📄 [flatten whole_netlist_insideu1 and u2.png](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/flatten%20whole_netlist_insideu1%20and%20u2.png)
    - 📄 [multiple_modules dotviewer.png](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/multiple_modules%20dotviewer.png)
    - 📄 [multiple_modules nand.png](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/multiple_modules%20nand.png)
    - 📄 [multiple_modules.png](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/multiple_modules.png)
    - 📄 [multiple_modules2.png](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/multiple_modules2.png)
    - 📄 [multiple_modules3.png](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/multiple_modules3.png)
    - 📄 [README.md](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/README.md)
    - 📄 [synth -top.png](Module%202/Lab5%20-%20%20Hier%20and%20flat%20synth/synth%20-top.png)
  - 📁 **[Lab6 - Flipflop synthesis and simulation/](Module%202/Lab6%20-%20Flipflop%20synthesis%20and%20simulation/)**
    - 📄 [async dotlib changed.png](Module%202/Lab6%20-%20Flipflop%20synthesis%20and%20simulation/async%20dotlib%20changed.png)
    - 📄 [async dotlib.png](Module%202/Lab6%20-%20Flipflop%20synthesis%20and%20simulation/async%20dotlib.png)
    - 📄 [crosscheck.png](Module%202/Lab6%20-%20Flipflop%20synthesis%20and%20simulation/crosscheck.png)
    - 📄 [files used.png](Module%202/Lab6%20-%20Flipflop%20synthesis%20and%20simulation/files%20used.png)
    - 📄 [lab_asynch ff.png](Module%202/Lab6%20-%20Flipflop%20synthesis%20and%20simulation/lab_asynch%20ff.png)
    - 📄 [README.md](Module%202/Lab6%20-%20Flipflop%20synthesis%20and%20simulation/README.md)
    - 📄 [sync and async.png](Module%202/Lab6%20-%20Flipflop%20synthesis%20and%20simulation/sync%20and%20async.png)
    - 📄 [tb_async.png](Module%202/Lab6%20-%20Flipflop%20synthesis%20and%20simulation/tb_async.png)
  - 📁 **[Lab7 - Intresting optimisations/](Module%202/Lab7%20-%20Intresting%20optimisations/)**
    - 📄 [gvim crosscheck of mul2_net.png](Module%202/Lab7%20-%20Intresting%20optimisations/gvim%20crosscheck%20of%20mul2_net.png)
    - 📄 [mult2 dotviewer.png](Module%202/Lab7%20-%20Intresting%20optimisations/mult2%20dotviewer.png)
    - 📄 [mult2 explanation.png](Module%202/Lab7%20-%20Intresting%20optimisations/mult2%20explanation.png)
    - 📄 [README.md](Module%202/Lab7%20-%20Intresting%20optimisations/README.md)
    - 📄 [Screenshot 2026-08-09 183302.png](Module%202/Lab7%20-%20Intresting%20optimisations/Screenshot%202026-08-09%20183302.png)
- 📁 **[Module 3/](Module%203/)**
  - 📁 **[1_Introduction to Optimisation/](Module%203/1_Introduction%20to%20Optimisation/)**
    - 📄 [Boolean logic op.png](Module%203/1_Introduction%20to%20Optimisation/Boolean%20logic%20op.png)
    - 📄 [combinational logic optimisation.png](Module%203/1_Introduction%20to%20Optimisation/combinational%20logic%20optimisation.png)
    - 📄 [constant logic op.png](Module%203/1_Introduction%20to%20Optimisation/constant%20logic%20op.png)
    - 📄 [README.md](Module%203/1_Introduction%20to%20Optimisation/README.md)
    - 📄 [sequential constant.png](Module%203/1_Introduction%20to%20Optimisation/sequential%20constant.png)
    - 📄 [Sequential logic optimisation.png](Module%203/1_Introduction%20to%20Optimisation/Sequential%20logic%20optimisation.png)
    - 📄 [State, cloning and retiming.png](Module%203/1_Introduction%20to%20Optimisation/State%2C%20cloning%20and%20retiming.png)
  - 📁 **[2_Optimisation/](Module%203/2_Optimisation/)**
    - 📄 [opt_check.png](Module%203/2_Optimisation/opt_check.png)
    - 📄 [opt_check2.png](Module%203/2_Optimisation/opt_check2.png)
    - 📄 [opt_check3.png](Module%203/2_Optimisation/opt_check3.png)
    - 📄 [README.md](Module%203/2_Optimisation/README.md)
  - 📁 **[3_Sequential optimisation techniques/](Module%203/3_Sequential%20optimisation%20techniques/)**
    - 📄 [dff_const1.png](Module%203/3_Sequential%20optimisation%20techniques/dff_const1.png)
    - 📄 [dffconst1_dotviewer.png](Module%203/3_Sequential%20optimisation%20techniques/dffconst1_dotviewer.png)
    - 📄 [dffconst3.png](Module%203/3_Sequential%20optimisation%20techniques/dffconst3.png)
    - 📄 [dffconst3_dotviewer.png](Module%203/3_Sequential%20optimisation%20techniques/dffconst3_dotviewer.png)
    - 📄 [dffconst_2 dotviewer.png](Module%203/3_Sequential%20optimisation%20techniques/dffconst_2%20dotviewer.png)
    - 📄 [README.md](Module%203/3_Sequential%20optimisation%20techniques/README.md)
  - 📁 **[4_Unused output optimisation/](Module%203/4_Unused%20output%20optimisation/)**
    - 📄 [Changed_counter_opt.png](Module%203/4_Unused%20output%20optimisation/Changed_counter_opt.png)
    - 📄 [combinational logic optimisation.png](Module%203/4_Unused%20output%20optimisation/combinational%20logic%20optimisation.png)
    - 📄 [constant logic op.png](Module%203/4_Unused%20output%20optimisation/constant%20logic%20op.png)
    - 📄 [counter_opt.png](Module%203/4_Unused%20output%20optimisation/counter_opt.png)
    - 📄 [README.md](Module%203/4_Unused%20output%20optimisation/README.md)
- 📁 **[Module 4/](Module%204/)**
  - 📁 **[1_Intro to GLS & Synthesis simulation mismatches/](Module%204/1_Intro%20to%20GLS%20%26%20Synthesis%20simulation%20mismatches/)**
    - 📄 [Blocking and non-blocking.png](Module%204/1_Intro%20to%20GLS%20%26%20Synthesis%20simulation%20mismatches/Blocking%20and%20non-blocking.png)
    - 📄 [caveat with blocking statements.png](Module%204/1_Intro%20to%20GLS%20%26%20Synthesis%20simulation%20mismatches/caveat%20with%20blocking%20statements.png)
    - 📄 [GLS using iverilog.png](Module%204/1_Intro%20to%20GLS%20%26%20Synthesis%20simulation%20mismatches/GLS%20using%20iverilog.png)
    - 📄 [GLS.png](Module%204/1_Intro%20to%20GLS%20%26%20Synthesis%20simulation%20mismatches/GLS.png)
    - 📄 [Missing sensitivity list.png](Module%204/1_Intro%20to%20GLS%20%26%20Synthesis%20simulation%20mismatches/Missing%20sensitivity%20list.png)
    - 📄 [README.md](Module%204/1_Intro%20to%20GLS%20%26%20Synthesis%20simulation%20mismatches/README.md)
    - 📄 [Syth simulation mismatch.png](Module%204/1_Intro%20to%20GLS%20%26%20Synthesis%20simulation%20mismatches/Syth%20simulation%20mismatch.png)
    - 📄 [What we are trying to do with GLS.png](Module%204/1_Intro%20to%20GLS%20%26%20Synthesis%20simulation%20mismatches/What%20we%20are%20trying%20to%20do%20with%20GLS.png)
  - 📁 **[2_GLS | Synth sim | Mismatch LAB/](Module%204/2_GLS%20%7C%20Synth%20sim%20%7C%20Mismatch%20LAB/)**
    - 📄 [bad_mux.png](Module%204/2_GLS%20%7C%20Synth%20sim%20%7C%20Mismatch%20LAB/bad_mux.png)
    - 📄 [gls_bad_mux.png](Module%204/2_GLS%20%7C%20Synth%20sim%20%7C%20Mismatch%20LAB/gls_bad_mux.png)
    - 📄 [gls_ternary_op.png](Module%204/2_GLS%20%7C%20Synth%20sim%20%7C%20Mismatch%20LAB/gls_ternary_op.png)
    - 📄 [README.md](Module%204/2_GLS%20%7C%20Synth%20sim%20%7C%20Mismatch%20LAB/README.md)
    - 📄 [synth_netlist_ternary_op.png](Module%204/2_GLS%20%7C%20Synth%20sim%20%7C%20Mismatch%20LAB/synth_netlist_ternary_op.png)
    - 📄 [ternary_operator.png](Module%204/2_GLS%20%7C%20Synth%20sim%20%7C%20Mismatch%20LAB/ternary_operator.png)
  - 📁 **[3_Blocking caveat/](Module%204/3_Blocking%20caveat/)**
    - 📄 [blocking_caveat.png](Module%204/3_Blocking%20caveat/blocking_caveat.png)
    - 📄 [blocking_caveat_netlist.png](Module%204/3_Blocking%20caveat/blocking_caveat_netlist.png)
    - 📄 [README.md](Module%204/3_Blocking%20caveat/README.md)
    - 📄 [synth_mismatch_blocking_caveat.png](Module%204/3_Blocking%20caveat/synth_mismatch_blocking_caveat.png)
- 📁 **[Module 5/](Module%205/)**
  - 📁 **[1_If Case constructs/](Module%205/1_If%20Case%20constructs/)**
    - 📄 [Case statement.png](Module%205/1_If%20Case%20constructs/Case%20statement.png)
    - 📄 [Dangers of case1.png](Module%205/1_If%20Case%20constructs/Dangers%20of%20case1.png)
    - 📄 [Dangers of case2.png](Module%205/1_If%20Case%20constructs/Dangers%20of%20case2.png)
    - 📄 [Dangers of if.png](Module%205/1_If%20Case%20constructs/Dangers%20of%20if.png)
    - 📄 [if statement.png](Module%205/1_If%20Case%20constructs/if%20statement.png)
    - 📄 [README.md](Module%205/1_If%20Case%20constructs/README.md)
  - 📁 **[2_If statements/](Module%205/2_If%20statements/)**
    - 📄 [incomp_if.png](Module%205/2_If%20statements/incomp_if.png)
    - 📄 [incomp_if2.png](Module%205/2_If%20statements/incomp_if2.png)
    - 📄 [README.md](Module%205/2_If%20statements/README.md)
    - 📄 [synth_incomp_if.png](Module%205/2_If%20statements/synth_incomp_if.png)
    - 📄 [synth_incomp_if2.png](Module%205/2_If%20statements/synth_incomp_if2.png)
  - 📁 **[3_case_statements/](Module%205/3_case_statements/)**
    - 📄 [bad_case.png](Module%205/3_case_statements/bad_case.png)
    - 📄 [comp_case.png](Module%205/3_case_statements/comp_case.png)
    - 📄 [gls_bad_case.png](Module%205/3_case_statements/gls_bad_case.png)
    - 📄 [incomp_case.png](Module%205/3_case_statements/incomp_case.png)
    - 📄 [partial_case.png](Module%205/3_case_statements/partial_case.png)
    - 📄 [README.md](Module%205/3_case_statements/README.md)
    - 📄 [synth_compcase.png](Module%205/3_case_statements/synth_compcase.png)
    - 📄 [synth_incomp_case.png](Module%205/3_case_statements/synth_incomp_case.png)
  - 📁 **[4_loop constraints/](Module%205/4_loop%20constraints/)**
    - 📄 [README.md](Module%205/4_loop%20constraints/README.md)

## Part 2 – Physical Design 🏗️

*(`Module 6`–`10`)*

- 📁 **[Module 6/](Module%206/)**
  - 📁 **[1_How to talk to computers/](Module%206/1_How%20to%20talk%20to%20computers/)**
    - 📄 [3 steps.png](Module%206/1_How%20to%20talk%20to%20computers/3%20steps.png)
    - 📄 [Foundaries and Macros.png](Module%206/1_How%20to%20talk%20to%20computers/Foundaries%20and%20Macros.png)
    - 📄 [Into to RISC-V architecture.png](Module%206/1_How%20to%20talk%20to%20computers/Into%20to%20RISC-V%20architecture.png)
    - 📄 [intro to chip layout.png](Module%206/1_How%20to%20talk%20to%20computers/intro%20to%20chip%20layout.png)
    - 📄 [README.md](Module%206/1_How%20to%20talk%20to%20computers/README.md)
    - 📄 [software to hardware.png](Module%206/1_How%20to%20talk%20to%20computers/software%20to%20hardware.png)
  - 📁 **[2_SoC design and Openlane/](Module%206/2_SoC%20design%20and%20Openlane/)**
    - 📄 [eda tools.png](Module%206/2_SoC%20design%20and%20Openlane/eda%20tools.png)
    - 📄 [Intro to openlane.png](Module%206/2_SoC%20design%20and%20Openlane/Intro%20to%20openlane.png)
    - 📄 [Intro to soc design using openlane.png](Module%206/2_SoC%20design%20and%20Openlane/Intro%20to%20soc%20design%20using%20openlane.png)
    - 📄 [Open sourse history.png](Module%206/2_SoC%20design%20and%20Openlane/Open%20sourse%20history.png)
    - 📄 [openlane asic flow.png](Module%206/2_SoC%20design%20and%20Openlane/openlane%20asic%20flow.png)
    - 📄 [README.md](Module%206/2_SoC%20design%20and%20Openlane/README.md)
    - 📄 [simplified rtl to gdsii flow.png](Module%206/2_SoC%20design%20and%20Openlane/simplified%20rtl%20to%20gdsii%20flow.png)
  - 📁 **[3_Lab- Getting to know Openlane/](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/)**
    - 📄 [Config file.png](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/Config%20file.png)
    - 📄 [Invoking Openlane.png](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/Invoking%20Openlane.png)
    - 📄 [less config.tcl.png](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/less%20config.tcl.png)
    - 📄 [Merged_lef.png](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/Merged_lef.png)
    - 📄 [Merging LEFS.png](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/Merging%20LEFS.png)
    - 📄 [Netlist.png](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/Netlist.png)
    - 📄 [Openlane design files.png](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/Openlane%20design%20files.png)
    - 📄 [README.md](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/README.md)
    - 📄 [Report.png](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/Report.png)
    - 📄 [Synthesised.png](Module%206/3_Lab-%20Getting%20to%20know%20Openlane/Synthesised.png)
- 📁 **[Module 7/](Module%207/)**
  - 📁 **[1_Chip Floor Planning/](Module%207/1_Chip%20Floor%20Planning/)**
    - 📄 [Black boxes.png](Module%207/1_Chip%20Floor%20Planning/Black%20boxes.png)
    - 📄 [Checking layers.png](Module%207/1_Chip%20Floor%20Planning/Checking%20layers.png)
    - 📄 [Core and Die.png](Module%207/1_Chip%20Floor%20Planning/Core%20and%20Die.png)
    - 📄 [Decoupling capacitor.png](Module%207/1_Chip%20Floor%20Planning/Decoupling%20capacitor.png)
    - 📄 [Floorplan def file.png](Module%207/1_Chip%20Floor%20Planning/Floorplan%20def%20file.png)
    - 📄 [ioPlace log.png](Module%207/1_Chip%20Floor%20Planning/ioPlace%20log.png)
    - 📄 [layout.png](Module%207/1_Chip%20Floor%20Planning/layout.png)
    - 📄 [Pin_Placement.png](Module%207/1_Chip%20Floor%20Planning/Pin_Placement.png)
    - 📄 [Powerplanning.png](Module%207/1_Chip%20Floor%20Planning/Powerplanning.png)
    - 📄 [Powerplanning2.png](Module%207/1_Chip%20Floor%20Planning/Powerplanning2.png)
    - 📄 [Preplaces cells.png](Module%207/1_Chip%20Floor%20Planning/Preplaces%20cells.png)
    - 📄 [README.md](Module%207/1_Chip%20Floor%20Planning/README.md)
    - 📄 [Sky130 config file.png](Module%207/1_Chip%20Floor%20Planning/Sky130%20config%20file.png)
    - 📄 [Utilisation ratio and ascpect ration.png](Module%207/1_Chip%20Floor%20Planning/Utilisation%20ratio%20and%20ascpect%20ration.png)
    - 📄 [Variables for floorplanning.png](Module%207/1_Chip%20Floor%20Planning/Variables%20for%20floorplanning.png)
    - 📄 [Variables for synthesis.png](Module%207/1_Chip%20Floor%20Planning/Variables%20for%20synthesis.png)
    - 📄 [Width and length.png](Module%207/1_Chip%20Floor%20Planning/Width%20and%20length.png)
  - 📁 **[2_Library binding and Placement/](Module%207/2_Library%20binding%20and%20Placement/)**
    - 📄 [Checking layers.png](Module%207/2_Library%20binding%20and%20Placement/Checking%20layers.png)
    - 📄 [Example circuit.png](Module%207/2_Library%20binding%20and%20Placement/Example%20circuit.png)
    - 📄 [Flavours of shapes.png](Module%207/2_Library%20binding%20and%20Placement/Flavours%20of%20shapes.png)
    - 📄 [layout.png](Module%207/2_Library%20binding%20and%20Placement/layout.png)
    - 📄 [Layout_floorplan.png](Module%207/2_Library%20binding%20and%20Placement/Layout_floorplan.png)
    - 📄 [Optimizing placement with buffers.png](Module%207/2_Library%20binding%20and%20Placement/Optimizing%20placement%20with%20buffers.png)
    - 📄 [README.md](Module%207/2_Library%20binding%20and%20Placement/README.md)
    - 📄 [Steps of logic synthesis.png](Module%207/2_Library%20binding%20and%20Placement/Steps%20of%20logic%20synthesis.png)
    - 📄 [tkcon 2.3 Main.png](Module%207/2_Library%20binding%20and%20Placement/tkcon%202.3%20Main.png)
  - 📁 **[3_4_Cell design flow and Timing charecterisation/](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/)**
    - 📄 [8 steps.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/8%20steps.png)
    - 📄 [Cel design flow inputs.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/Cel%20design%20flow%20inputs.png)
    - 📄 [cell design recap.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/cell%20design%20recap.png)
    - 📄 [design steps and outputs.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/design%20steps%20and%20outputs.png)
    - 📄 [Guna.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/Guna.png)
    - 📄 [Layout with stick diagram.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/Layout%20with%20stick%20diagram.png)
    - 📄 [Outputs.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/Outputs.png)
    - 📄 [Propogation delay.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/Propogation%20delay.png)
    - 📄 [README.md](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/README.md)
    - 📄 [Timing threshold definitions.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/Timing%20threshold%20definitions.png)
    - 📄 [transition time.png](Module%207/3_4_Cell%20design%20flow%20and%20Timing%20charecterisation/transition%20time.png)
- 📁 **[Module 8/](Module%208/)**
  - 📁 **[1_Cmos inverter/](Module%208/1_Cmos%20inverter/)**
    - 📄 [equidistant pins.png](Module%208/1_Cmos%20inverter/equidistant%20pins.png)
    - 📄 [inverter layout.png](Module%208/1_Cmos%20inverter/inverter%20layout.png)
    - 📄 [README.md](Module%208/1_Cmos%20inverter/README.md)
    - 📄 [spice deck creation 1.png](Module%208/1_Cmos%20inverter/spice%20deck%20creation%201.png)
    - 📄 [Spice deck2.png](Module%208/1_Cmos%20inverter/Spice%20deck2.png)
    - 📄 [spice wave form.png](Module%208/1_Cmos%20inverter/spice%20wave%20form.png)
    - 📄 [Stacked pins.png](Module%208/1_Cmos%20inverter/Stacked%20pins.png)
    - 📄 [static and dynamic .png](Module%208/1_Cmos%20inverter/static%20and%20dynamic%20.png)
    - 📄 [switching threshhold.png](Module%208/1_Cmos%20inverter/switching%20threshhold.png)
    - 📄 [technological paramenters of cmos.png](Module%208/1_Cmos%20inverter/technological%20paramenters%20of%20cmos.png)
    - 📄 [waveforms compasision.png](Module%208/1_Cmos%20inverter/waveforms%20compasision.png)
  - 📁 **[2_CMOS fabrication/](Module%208/2_CMOS%20fabrication/)**
    - 📄 [box dimentions.png](Module%208/2_CMOS%20fabrication/box%20dimentions.png)
    - 📄 [Checking type of layer and extracting.png](Module%208/2_CMOS%20fabrication/Checking%20type%20of%20layer%20and%20extracting.png)
    - 📄 [CMOS done.png](Module%208/2_CMOS%20fabrication/CMOS%20done.png)
    - 📄 [CMOS Inverter layers.png](Module%208/2_CMOS%20fabrication/CMOS%20Inverter%20layers.png)
    - 📄 [Cmosfab1.png](Module%208/2_CMOS%20fabrication/Cmosfab1.png)
    - 📄 [Cmosfab2.png](Module%208/2_CMOS%20fabrication/Cmosfab2.png)
    - 📄 [Cmosfab3.2.png](Module%208/2_CMOS%20fabrication/Cmosfab3.2.png)
    - 📄 [Cmosfab3.png](Module%208/2_CMOS%20fabrication/Cmosfab3.png)
    - 📄 [Cmosfab4.png](Module%208/2_CMOS%20fabrication/Cmosfab4.png)
    - 📄 [Cmosfab5.2.png](Module%208/2_CMOS%20fabrication/Cmosfab5.2.png)
    - 📄 [Cmosfab5.png](Module%208/2_CMOS%20fabrication/Cmosfab5.png)
    - 📄 [Cmosfab6.png](Module%208/2_CMOS%20fabrication/Cmosfab6.png)
    - 📄 [Cmosfab7.png](Module%208/2_CMOS%20fabrication/Cmosfab7.png)
    - 📄 [Cmosfab8.png](Module%208/2_CMOS%20fabrication/Cmosfab8.png)
    - 📄 [layers labelling.png](Module%208/2_CMOS%20fabrication/layers%20labelling.png)
    - 📄 [README.md](Module%208/2_CMOS%20fabrication/README.md)
    - 📄 [technological paramenters of cmos.png](Module%208/2_CMOS%20fabrication/technological%20paramenters%20of%20cmos.png)
  - 📁 **[3_Tech file labs/](Module%208/3_Tech%20file%20labs/)**
    - 📄 [charecterising cell.png](Module%208/3_Tech%20file%20labs/charecterising%20cell.png)
    - 📄 [charecterising cell2.png](Module%208/3_Tech%20file%20labs/charecterising%20cell2.png)
    - 📄 [exersise 1.png](Module%208/3_Tech%20file%20labs/exersise%201.png)
    - 📄 [exersise 2.png](Module%208/3_Tech%20file%20labs/exersise%202.png)
    - 📄 [final spice deck.png](Module%208/3_Tech%20file%20labs/final%20spice%20deck.png)
    - 📄 [final spice deck2.png](Module%208/3_Tech%20file%20labs/final%20spice%20deck2.png)
    - 📄 [implementing poly resistor spacing.png](Module%208/3_Tech%20file%20labs/implementing%20poly%20resistor%20spacing.png)
    - 📄 [incorrect rule.png](Module%208/3_Tech%20file%20labs/incorrect%20rule.png)
    - 📄 [indtroduction to sky130 pdks.png](Module%208/3_Tech%20file%20labs/indtroduction%20to%20sky130%20pdks.png)
    - 📄 [Magic tool option and drc rules.png](Module%208/3_Tech%20file%20labs/Magic%20tool%20option%20and%20drc%20rules.png)
    - 📄 [README.md](Module%208/3_Tech%20file%20labs/README.md)
    - 📄 [Using simple tools.png](Module%208/3_Tech%20file%20labs/Using%20simple%20tools.png)
- 📁 **[Module 9/](Module%209/)**
  - 📄 [CMOS done.png](Module%209/CMOS%20done.png)
  - 📄 [Defining ports.png](Module%209/Defining%20ports.png)
  - 📄 [delay tables.png](Module%209/delay%20tables.png)
  - 📄 [delay tables_1.png](Module%209/delay%20tables_1.png)
  - 📄 [grids.png](Module%209/grids.png)
  - 📄 [important commands.png](Module%209/important%20commands.png)
  - 📄 [lef file.png](Module%209/lef%20file.png)
  - 📄 [library of all cells.png](Module%209/library%20of%20all%20cells.png)
  - 📄 [openlane.png](Module%209/openlane.png)
  - 📄 [README.md](Module%209/README.md)
  - 📄 [tracks.png](Module%209/tracks.png)
- 📁 **[Module-10/](Module-10/)**
  - 📁 **[Classwork/](Module-10/Classwork/)**
    - 📄 [DRC clean 6.png](Module-10/Classwork/DRC%20clean%206.png)
    - 📄 [DRC via width.png](Module-10/Classwork/DRC%20via%20width.png)
    - 📄 [DRC violation.png](Module-10/Classwork/DRC%20violation.png)
    - 📄 [DRC wire pinch.png](Module-10/Classwork/DRC%20wire%20pinch.png)
    - 📄 [DRC wire spacing.png](Module-10/Classwork/DRC%20wire%20spacing.png)
    - 📄 [LEE's algorithm 2.png](Module-10/Classwork/LEE%27s%20algorithm%202.png)
    - 📄 [Parasitics extraction.png](Module-10/Classwork/Parasitics%20extraction.png)
    - 📄 [Preprocessed route guides.png](Module-10/Classwork/Preprocessed%20route%20guides.png)
    - 📄 [README.md](Module-10/Classwork/README.md)
    - 📄 [Routing - LEE'S algorithm.png](Module-10/Classwork/Routing%20-%20LEE%27S%20algorithm.png)
    - 📄 [Routing overview.png](Module-10/Classwork/Routing%20overview.png)
    - 📄 [Triton route.png](Module-10/Classwork/Triton%20route.png)

---

- 📄 [README.md](README.md)
