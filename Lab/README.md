# VSDBabySoC Design and Verification Guide
***

## Introduction: VSDBabySoC Overview

VSDBabySoC is a compact, educational SoC integrating RVMYTH (RISC-V CPU), high-multiplication PLL, and a 10-bit DAC. Its key aim is reliable digital-analog integration and IP calibration for comprehensive hardware experimentation.

## System Details and Components

- **RVMYTH**: RISC-V CPU for digital processing.
- **PLL**: 8x multiplier Phase-Locked Loop for clock stability.
- **DAC**: 10-bit precision Digital-to-Analog Converter for external analog interfacing.

<img width="1248" height="698" alt="image" src="https://github.com/user-attachments/assets/251c13e7-a06f-4ff9-a137-ac15bf674a56" />
 
  

***

## Problem Statement

This guide develops a diminutive open-source SoC allowing digital RISC-V computation, robust clocking, and direct analog interfacing for TV/mobile applications via Sky130 technology. The documentation focuses on hands-on learning and practical verification.

***

## Essential Concepts

- **SoC Definition**: A chip integrating digital/analog IPs for versatile embedded tasks.
- **RVMYTH**: Educational RISC-V CPU core for small-scale applications.
- **PLL**: Synchronizes and stabilizes system clock signals.
- **DAC**: Translates digital outputs to analog signals for real-world devices.

***

## Directory and Project Structure

```txt
VSDBabySoC/
├── src/
│   ├── include/
│   └── module/
└── output/
└── compiled_tlv/
```

***

## Environment Setup and Repository Cloning

To start, prepare the workspace and clone the project:

```bash
mkdir VLSI
cd ~/VLSI
git clone https://github.com/manili/VSDBabySoC.git
cd VSDBabySoC
ls src/module/
```
<img width="817" height="401" alt="image" src="https://github.com/user-attachments/assets/7c9f22b0-dd3e-4862-b5db-19103d030d5b" />

Verify the presence of essential modules in the directory.

***

## TLV-to-Verilog Conversion for RVMYTH

Convert TL-Verilog to Verilog for simulation as follows:

```bash
# Step 1: Install python3-venv (if not already installed)
sudo apt update
sudo apt install python3-venv python3-pip

# Step 2: Create and activate a virtual environment
cd ~/VLSI/VSDBabySoC/
python3 -m venv sp_env
source sp_env/bin/activate

# Step 3: Install SandPiper-SaaS inside the virtual environment
pip install pyyaml click sandpiper-saas

# Step 4: Convert rvmyth.tlv to Verilog
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/

# Step 5: Deactivate the environment
deactivate
```
## Log
```bash
vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ python3 -m venv sp_env
vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ source sp_env/bin/activate
(sp_env) vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ pip install pyyaml click sandpiper-saas
Collecting pyyaml
  Using cached pyyaml-6.0.3-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl.metadata (2.4 kB)
Collecting click
  Using cached click-8.3.0-py3-none-any.whl.metadata (2.6 kB)
Collecting sandpiper-saas
  Using cached sandpiper_saas-1.1.0-py3-none-any.whl.metadata (1.7 kB)
Collecting Path (from sandpiper-saas)
  Using cached path-17.1.1-py3-none-any.whl.metadata (6.5 kB)
Collecting argparse (from sandpiper-saas)
  Using cached argparse-1.4.0-py2.py3-none-any.whl.metadata (2.8 kB)
Collecting requests (from sandpiper-saas)
  Using cached requests-2.32.5-py3-none-any.whl.metadata (4.9 kB)
Collecting charset_normalizer<4,>=2 (from requests->sandpiper-saas)
  Using cached charset_normalizer-3.4.3-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl.metadata (36 kB)
Collecting idna<4,>=2.5 (from requests->sandpiper-saas)
  Using cached idna-3.10-py3-none-any.whl.metadata (10 kB)
Collecting urllib3<3,>=1.21.1 (from requests->sandpiper-saas)
  Using cached urllib3-2.5.0-py3-none-any.whl.metadata (6.5 kB)
Collecting certifi>=2017.4.17 (from requests->sandpiper-saas)
  Using cached certifi-2025.8.3-py3-none-any.whl.metadata (2.4 kB)
Using cached pyyaml-6.0.3-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (807 kB)
Using cached click-8.3.0-py3-none-any.whl (107 kB)
Using cached sandpiper_saas-1.1.0-py3-none-any.whl (5.3 kB)
Using cached argparse-1.4.0-py2.py3-none-any.whl (23 kB)
Using cached path-17.1.1-py3-none-any.whl (23 kB)
Using cached requests-2.32.5-py3-none-any.whl (64 kB)
Using cached certifi-2025.8.3-py3-none-any.whl (161 kB)
Using cached charset_normalizer-3.4.3-cp312-cp312-manylinux2014_x86_64.manylinux_2_17_x86_64.manylinux_2_28_x86_64.whl (151 kB)
Using cached idna-3.10-py3-none-any.whl (70 kB)
Using cached urllib3-2.5.0-py3-none-any.whl (129 kB)
Installing collected packages: argparse, urllib3, pyyaml, Path, idna, click, charset_normalizer, certifi, requests, sandpiper-saas
Successfully installed Path-17.1.1 argparse-1.4.0 certifi-2025.8.3 charset_normalizer-3.4.3 click-8.3.0 idna-3.10 pyyaml-6.0.3 requests-2.32.5 sandpiper-saas-1.1.0 urllib3-2.5.0
(sp_env) vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
You have agreed to our Terms of Service here: https://makerchip.com/terms.
INFORM(0) (PROD_INFO):
	SandPiper(TM) 1.14-2022/10/10-beta-Pro from Redwood EDA, LLC
	(DEV) Run as: "java -jar sandpiper.jar --bestsv --noline -p verilog --outdir=out --nopath -i ./rvmyth.m4out.tlv -o rvmyth.v
	For help, including product info, run with -h.

INFORM(0) (LICENSE):
	Licensed to "Redwood EDA, LLC" as: Full Edition.

INFORM(0) (FILES):
	Reading "./rvmyth.m4out.tlv"
	to produce:
		Translated HDL File: "out/rvmyth.v"
		Generated HDL File: "out/rvmyth_gen.v"

(sp_env) vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC$ 
```

```txt
ls src/module/
vsdtapeout@pathanrehman:~/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module$ ls
avsddac.v   pseudo_rand_gen.sv  rvmyth.tlv                       testbench.v
avsdpll.v   pseudo_rand.sv      rvmyth.v                         vsdbabysoc.v
clk_gate.v  rvmyth_gen.v        testbench.rvmyth.post-routing.v
```

***

## Simulation Workflow

### Pre-Synthesis Simulation Steps

Setup output directory and run simulation:

```bash
cd ~/VLSI/VSDBabySoC/
mkdir -p output/pre_synth_sim
iverilog -o /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/output/pre_synth_sim/pre_synth_sim.out -DPRE_SYNTH_SIM -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/include -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/testbench.v
```
<img width="814" height="650" alt="image" src="https://github.com/user-attachments/assets/dd0d6ec9-1f74-44fc-ad73-e1264f20a65d" />
***

### Waveform Analysis in GTKWave

Open the VCD file for signal visualization:

```bash
cd output/pre_synth_sim
./pre_synth_sim.out
```

### Simulation Log

[Read Here](https://github.com/Pathan-Rehman/PathanRehman_RISC-V-SoC-Tapeout-Program_VSD_Week_2/blob/main/Lab/SimulationLog.md)

### Waveform Viewing
```bash
gtkwave output/pre_synth_sim/pre_synth_sim.vcd
```
Drag relevant signals: CLK, reset, OUT (DAC), RV_TO_DAC[9:0].

<img width="1052" height="615" alt="image" src="https://github.com/user-attachments/assets/8191efa5-2070-41d8-9cd4-0b03922b8feb" />
 
This screenshot highlights the correct toggling behavior of the clock (periodic changes), the response to reset (initialization phase), and propagation of digital OUT and RV_TO_DAC values through the simulation cycle. This shows functional correctness and timing relationships between the components.

The signals shown in the figure are described as follows:  
- **CLK**: The clock input to the RVMYTH core, originally generated by the PLL.  
- **reset**: The reset input signal for the RVMYTH core, sourced externally.  
- **OUT**: The output signal from the VSDBabySoC module's DAC. Due to simulation limitations, this behaves digitally, which is not an accurate reflection of its true analog nature.  
- **RV_TO_DAC[9:0]**: The 10-bit output port from the RVMYTH core, which corresponds to the value stored in register #17.  
- **OUT (real datatype)**: A real-valued wire representing the DAC's analog output, which can be viewed by changing the signal's data format in the simulator to Analog → Step.

***

### DAC Analog Output Verification

Switch DAC OUT signal to analog mode in GTKWave.

<img width="960" height="779" alt="image" src="https://github.com/user-attachments/assets/a526d61b-9f98-49eb-9561-5bb16d7f7585" />


<img width="1056" height="608" alt="image" src="https://github.com/user-attachments/assets/d6bceaab-5181-4f01-b51b-599c29919774" />

 
Here, OUT (DAC) is displayed in analog step mode. The waveform confirms that digital values from RV_TO_DAC are correctly converted and output as stepped analog signals—demonstrating successful digital-to-analog interfacing in the BabySoC simulation.

This screenshot further illustrates sustained analog output transitions, showing smooth conversion and verification of 10-bit DAC resolution, vital for confirming signal fidelity.

***

## Troubleshooting

- **Module Redefinition Errors**: Avoid duplicating module includes.
- **Path Resolution Failures**: Double-check -I flags and explicit paths.

***

# Yosys Synthesis Tutorial for BabySoC

## Overview

This guide demonstrates the synthesis process of the BabySoC project using the Yosys Open SYnthesis Suite. It covers command usage, the correct handling of file paths, and provides solutions for common synthesis errors.

***

## Directory Structure

Make sure the following project structure is set up:

```
~/Desktop/labs/Week2/VLSI/VSDBabySoC/
├── src/
│   ├── include/           # Verilog include files
│   ├── module/            # Verilog modules (vsdbabysoc.v, clkgate.v, rvmyth.v, etc)
│   └── lib/               # Liberty files (sky130fdschdtt025C1v80.lib, avsddac.lib, avsdpll.lib)
```
All paths provided in commands below match those seen in actual flows.

***

## Step-by-Step Synthesis Flow

### 1. Launch Yosys

Start Yosys from your working directory:

```sh
cd ~/Desktop/labs/Week2/VLSI/VSDBabySoC/src
yosys
```

***

### 2. Load Liberty Cell Libraries

Load the technology cell library (example for Sky130):

```yosys
read_liberty -lib /home/vsdtapeout/Desktop/labs/Week_1/Day_1/VLSI/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -lib /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/avsddac.lib /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/avsdpll.lib
```
<img width="822" height="610" alt="image" src="https://github.com/user-attachments/assets/09e61736-eae1-402f-879f-b65297e6f0e1" />

If the library contains definitions, you should see "Imported XXX cell types from liberty file".

***

### 3. Read Verilog Source Files

Indicate SV (SystemVerilog) support and all include/module paths. Avoid typographical errors in commands or filenames:

```yosys
read_verilog -sv -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/include/ -I /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoc/src/module/ /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/vsdbabysoc.v /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/clk_gate.v /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/module/rvmyth.v
```
<img width="823" height="609" alt="image" src="https://github.com/user-attachments/assets/22ea9913-9278-4f4b-893d-068893e53331" />

The above paths must exist; adjust them as per your actual directory. If successful, you'll see "Successfully finished Verilog frontend".

***

### 4. Specify the Top Module

Set the top-level module for synthesis (usually `vsdbabysoc`):

```yosys
synth -top vsdbabysoc
```
<img width="827" height="789" alt="image" src="https://github.com/user-attachments/assets/ac6fbf92-d994-4b22-b39b-270372b875fa" />

This will trigger module hierarchy and process netlist conversion with messages such as "Analyzing design hierarchy... Top module Used module..." and "Creating decoders for process...".

***

### 5. Technology Mapping

Map RTL to gates using ABC and techmap:

```yosys
# Automatic, as part of 'synth'
```
Expect log reports with extracted gate counts and optimized modules (e.g., "Extracted 4089 gates and 5280 wires to a netlist network with 1188 inputs and 216 outputs").

***

### 6. Run Design Checks

```yosys
check
```
<img width="603" height="212" alt="image" src="https://github.com/user-attachments/assets/4a70ce88-d118-40e6-a099-60826a35abfb" />

This checks for obvious structural problems in your synthesized design.

***

### 7. Write the Synthesized Netlist

Export your final synthesized Verilog netlist:

```yosys
write_verilog vsdbabysoc_synth_net.v
abc -liberty /home/vsdtapeout/Desktop/labs/Week_2/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib 

```
Netlist files are typically written in the working directory.

***

### 8. Visualize the Synthesized Design

For visual inspection, use:

```yosys
show vsdbabysoc
```
<img width="1050" height="310" alt="image" src="https://github.com/user-attachments/assets/d6b5d48d-8936-47f4-8fd6-ebf0c63b0881" />
If multiple modules are present, specify only one module due to Graphviz format limitations ("ERROR: For formats different than 'ps' or 'dot' only one module must be selected"). By default, results are stored in `/home/vsdtapeout/.yosys_show.dot`.

***

## Common Errors & Solutions

| Error Message | Cause | Solution |
|---------------|-------|----------|
| `ERROR Missing function on output GCLK of cell ...` | Liberty file lacks function definition for some output | Fix .lib file or use correct version |
| `ERROR syntax error, unexpected TOKID ...` | File is not valid Verilog/SystemVerilog | Check syntax using a simulator (Icarus Verilog recommended) |
| `ERROR Cant open input file ... for reading No such file or directory` | File path typo, or file missing | Double-check directory and filenames |
| `ERROR Re-definition of module ...` | Module loaded twice | Ensure each file is loaded only once |
| `ERROR Cant open include file ...` | Include file missing or path wrong | Verify/include directory and file names |
| `ERROR Command syntax error No filename given.` | Syntax error in Yosys command | Follow documented syntax, use help |
| `WARNING: Font family 'Times-Roman' is not available, using 'Ubuntu Sans 11'` | Graphviz font not installed | Usually not fatal, just an info message |

***

## Tips for Successful Synthesis

- Validate Verilog modules in a simulator before Yosys synthesis to catch subtle syntax issues (Yosys parser is not very descriptive for errors).
- Always use absolute paths for scripts to avoid directory confusion.
- Organize modules, includes, and libraries separately for clarity.
- Read the log output for warnings about memory/register transformations or dead code removal.
- Use `check` for sanity of final netlist before downstream tools.

***

## References

- Yosys official documentation
- Synth logs and flow output

***

This tutorial should allow any user with access to the files and requisite Yosys/ABC/Graphviz dependencies to fully synthesize, check, and troubleshoot the BabySoC design with real module and cell library paths.

## Rationale for Verification Phases

- **Pre-Synthesis Simulation**: Validates RTL logic functionality in a zero-delay environment; helpful for initial debugging and cleaning up code errors.
- **Post-Synthesis Simulation (GLS)**: Simulates synthesized gate-level netlist for accurate timing validation and checks for dynamic mismatches or unintended hardware artifacts.
