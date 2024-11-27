## Features
- Support for S7-1200 and S7-1500
- CHR and ZN step tuning
- Runs in Siemens PLC-simulator
- Source code can be accessed and modified
- Overall simpler design then Siemens PID_Compact

##  Known issues
Step tuning only works if the process (input) is very stable, an abort mechanism is needed to stop tuning if the process is or becomes unstable.

## Process value simulator
A process value simulator function has been added to facilitate easier testing and simulation of the PID controller.

## Gui for easy testing
A TP1200 Comfort project has been added so that the functionality can be easily tested and compared with Siemens PID_Compact.
To be able to simulate and compare against the Siemens PID_Compact function, you need a s7-1x00 plc or Siemens PLCSIM Advanced.

## Usage Instructions
See LLCCA_PID Quick Start Manual

## Installation
Open the .zap19 file in Siemens TIA Portal 19

## Installation SCL-files
1. Open a Siemens TIA Portal 19 project.
2. Place the SCL files under "External source files."
3. Execute the "Generate blocks from source" menu item.

## License
LCC Automation AB / (c)Copyright 2024
Released under the MIT License
