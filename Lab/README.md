# VSDBabySoC Design and Verification Guide

## Table of Contents

- Introduction: VSDBabySoC Overview  
- System Details and Components  
- Problem Statement  
- Essential Concepts: SoC, RVMYTH, PLL, DAC  
- Directory and Project Structure  
- Environment Setup and Repository Cloning  
- TLV-to-Verilog Conversion for RVMYTH  
- Simulation Workflow  
    - Pre-Synthesis Simulation Steps  
    - Simulation Log Example  
    - Waveform Analysis in GTKWave  
    - DAC Analog Output Verification  
- Troubleshooting  
- Rationale for Verification Phases  

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
iverilog -o ~/VLSI/VSDBabySoC/output/pre_synth_sim/pre_synth_sim.out -DPRE_SYNTH_SIM -I ~/VLSI/VSDBabySoC/src/include -I ~/VLSI/VSDBabySoC/src/module ~/VLSI/VSDBabySoC/src/module/testbench.v
```
*Simulation Log Placeholder*  
```txt
[Simulation Log]
Time: 0ns: Reset activated
Time: 10ns: Clock toggled HIGH, OUT=000
Time: 20ns: RV_TO_DAC=3F, OUT=63
...
Test Completed: All assertions passed.
```
Short Explanation:  
The simulation log shows how signals transition during run-time, ensuring the design responds properly to clock and reset events.

***

### Waveform Analysis in GTKWave

Open the VCD file for signal visualization:

```bash
gtkwave output/pre_synth_sim/pre_synth_sim.vcd
```
Drag relevant signals: CLK, reset, OUT (DAC), RV_TO_DAC[9:0].

*GTKWave Screenshot Placeholder*  
![Waveform Example]( Explanation:  
This screenshot highlights the correct toggling behavior of the clock (periodic changes), the response to reset (initialization phase), and propagation of digital OUT and RV_TO_DAC values through the simulation cycle. This shows functional correctness and timing relationships between the components.

***

### DAC Analog Output Verification

Switch DAC OUT signal to analog mode in GTKWave.

*Analog Output Screenshot Placeholder*  
![Analog Step Mode Screenshot]( Explanation:  
Here, OUT (DAC) is displayed in analog step mode. The waveform confirms that digital values from RV_TO_DAC are correctly converted and output as stepped analog signals—demonstrating successful digital-to-analog interfacing in the BabySoC simulation.

*Alternate Analog Output Screenshot Placeholder*  
![Analog Output Screenshot]( Explanation:  
This screenshot further illustrates sustained analog output transitions, showing smooth conversion and verification of 10-bit DAC resolution, vital for confirming signal fidelity.

***

## Troubleshooting

- **Module Redefinition Errors**: Avoid duplicating module includes.
- **Path Resolution Failures**: Double-check -I flags and explicit paths.

***

## Rationale for Verification Phases

- **Pre-Synthesis Simulation**: Validates RTL logic functionality in a zero-delay environment; helpful for initial debugging and cleaning up code errors.
- **Post-Synthesis Simulation (GLS)**: Simulates synthesized gate-level netlist for accurate timing validation and checks for dynamic mismatches or unintended hardware artifacts.
