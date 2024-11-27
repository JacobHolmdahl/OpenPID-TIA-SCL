# LLCCA_PID Quick Start Manual

This manual provides a quick guide to using the LLCCA_PID function block for Siemens S7-1200/1500 PLCs. This function block implements a PID controller with step tuning capabilities.

## 1. Function Block Interface

The function block has the following inputs, outputs, and parameters:

**Inputs:**

*   `Setpoint`:  The desired value for the process variable. (Real)
*   `Input`: The current value of the process variable. (Real)
*   `ManualValue`: The output value when in manual mode. (Real)
*   `Reset`: A boolean signal to reset the integral term and filters. (Bool)

**Outputs:**

*   `Out`: The calculated output value of the PID controller. (Real)
*   `Terms`: A structure containing the individual PID terms:
    *   `p`: Proportional term (Real)
    *   `i`: Integral term (Real)
    *   `d`: Derivative term (Real)

**In-Out Parameters:**

*   `ioMode`:  The operating mode of the controller. (USInt)
    *   0: Inactive
    *   1: Step tuning
    *   2: Reserved
    *   3: Automatic
    *   4: Manual
*   `ioKp`: Proportional gain. (Real)
*   `ioTi`: Integral time in seconds. (Real)
*   `ioTd`: Derivative time in seconds. (Real)

## 2. Operating Modes

The LLCCA_PID function block supports the following operating modes:

*   **Inactive (0):** The controller output is set to 0.
*   **Step Tuning (1):**  The controller automatically determines PID parameters based on the process response to a step change in the output. This mode requires a stable process.
*   **Automatic (3):** The controller operates in automatic mode using the configured PID parameters.
*   **Manual (4):** The controller output is set to the `ManualValue` input.

## 3. Step Tuning

To perform step tuning:

    a. Set `ioMode` to 1.
    b. Ensure the process is stable.
    c. The controller will automatically initiate a step change in the output and analyze the process response to calculate PID parameters.
    d. Once tuning is complete, the controller will revert to the previous mode and the calculated `ioKp`, `ioTi`, and `ioTd` values will be updated.

## 4. Automatic Mode

In automatic mode:

    a. Set `ioMode` to 3.
    b. Provide the desired `Setpoint`.
    c. The controller will calculate the output based on the configured `ioKp`, `ioTi`, and `ioTd` values.

## 5. Manual Mode

In manual mode:

    a. Set `ioMode` to 4.
    b. Provide the desired output value in `ManualValue`.

## 6. Tuning Rules

The step tuning function uses predefined tuning rules to calculate PID parameters. You can select the desired rule by setting the `statAdvanced.tuningRule` parameter:

*   0: Chien–Hrones–Reswick (CHR) with 0% overshoot
*   1: CHR with 20% overshoot
*   11: Ziegler-Nichols (ZN) fast
*   12: ZN normal
*   13: ZN slow

## 7. Additional Parameters

The function block also provides additional parameters for advanced configuration:

*   `statAdvanced.outMax`: Maximum output value.
*   `statAdvanced.outMin`: Minimum output value.
*   `statAdvanced.inputFilter`: Time constant for the input filter.
*   `statAdvanced.derivateFilter`: Time constant for the derivative filter.

## 8. Example Implementation

```structured text
// Instance of the LLCCA_PID function block
myPID(Setpoint := 100.0, 
      Input := processValue, 
      ManualValue := 50.0, 
      Reset := false, 
      ioMode := 3, 
      ioKp := 2.5, 
      ioTi := 10.0, 
      ioTd := 1.0, 
      Out => controlOutput, 
      Terms => pidTerms);
