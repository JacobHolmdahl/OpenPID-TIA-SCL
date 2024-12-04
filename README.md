**LLCCA_PID Function Block**

**Overview**

The `LLCCA_PID` function block implements a PID (Proportional-Integral-Derivative) controller with step tuning functionality. It is designed for use in Siemens S7-1200 and S7-1500 PLCs.

**Features**

*   Support for S7-1200 and S7-1500
*   Chien–Hrones–Reswick and Ziegler-Nichols step tuning
*   Runs in Siemens PLC-simulator
*   Source code can be accessed and modified
*   Overall simpler design then Siemens PID_Compact

**Known Issues**

*   The step tuning only works if the process (input) is very stable.
*   An abort mechanism is needed to stop tuning if the process is or becomes unstable.

**Process Value Simulator**

A process value simulator function has been added to facilitate easier testing and simulation of the PID controller.

**GUI for Easy Testing**

A TP1200 Comfort project has been added so that the functionality can be easily tested and compared with Siemens PID_Compact.

**Usage Instructions**

Please refer to the LLCCA_PID Quick Start Manual.

**Installation**

*   Open the .zap19 file in Siemens TIA Portal 19.

**Installation SCL-files**

1.  Open a Siemens TIA Portal 19 project.
2.  Place the SCL files under "External source files."
3.  Execute the "Generate blocks from source" menu item.

**Code Overview**

The provided `LLCCA_PID_x_y_z` file contains the SCL (Structured Control Language) code for the `LLCCA_PID` function block. The code includes:

*   **Input Variables:** `Setpoint`, `Input`, `ManualValue`, `Reset`
*   **Output Variables:** `Out`, `Terms` (structure with `p`, `i`, `d` components)
*   **In-Out Variables:** `ioMode`, `ioKp`, `ioTi`, `ioTd`
*   **Internal Variables:** Various static and temporary variables for calculations and state management

**Functionality**

The code implements the following functionality:

*   **Modes:** Inactive, Step tuning, Reserved, Automatic, Manual
*   **Step Tuning:** Calculates PID parameters based on the process response to a step change in the output.
*   **PID Control:** Calculates the output based on the error between the setpoint and the input, using the configured PID parameters.
*   **Filtering:** Includes input filtering and derivative filtering to improve control performance.
*   **Anti-Integral Windup:** Prevents the integral term from becoming too large, which can cause instability.

**Additional Notes**

*   The code is well-structured and includes comments to explain the functionality.
*   The terminology of some variables and functions is taken from the Siemens PID_Compact controller.
*   The code is optimized for access and visibility.

**License**

LCC Automation AB / (c)Copyright 2024. Released under the MIT License.
