# Car Wiper Control System - Simulink Project

## Overview

This project simulates a Car Wiper Control System using MATLAB Simulink. It features two different implementations of the control logic: one using the Simulink Case block and another using multi-switches. The project demonstrates how to manage wiper operations based on selected modes and rain detection.

## System Description

### Inputs

The Wiper Control System is driven by three main inputs:

1. **Wiper Mode (`WiprMod`)**  
   Controls the operational mode of the wiper system:
   - **0: Off** - The wiper is turned off.
   - **1: Auto** - The wiper speed is automatically adjusted based on rain intensity.
   - **2: Low Speed** - The wiper operates at a low, constant speed.
   - **3: High Speed** - The wiper operates at a high, constant speed.

2. **Rain Sensor Error (`RainSnsrErr`)**  
   Indicates the status of the rain sensor:
   - **0: Normal** - The rain sensor is functioning correctly.
   - **1: Error** - There is a fault with the rain sensor.

3. **Wiper Speed Request (`WiprSpdReq`)**  
   Determines the required speed of the wiper in Auto mode. The speed levels range from 0 to 7, with higher values representing faster speeds:
   - **0** - Wiper off
   - **1 to 7** - Increasing wiper speeds

### Outputs

The Wiper Control System provides two main outputs:

1. **Wiper Motor PWM Duty Cycle (`WiprMotPwmDutyCyc`)**  
   This output is a PWM command sent to the wiper motor, controlling its speed and activation based on the input conditions.

2. **Wiper Activation (`WiprActv`)**  
   Indicates whether the wiper motor is running or stopped:
   - **0: Stop** - The wiper motor is not activated.
   - **1: Running** - The wiper motor is activated.

### Processing Logic

The system processes the inputs to generate appropriate outputs as follows:

- **Off Mode (`WiprMod = 0`):**  
  The wiper motor is stopped (`WiprMotPwmDutyCyc = 0%`).

- **Auto Mode (`WiprMod = 1`):**  
  - **Rain Sensor Error (`RainSnsrErr = 1`):**  
    If there is a rain sensor error, the wiper motor is stopped (`WiprMotPwmDutyCyc = 0%`).
  - **No Rain Sensor Error (`RainSnsrErr = 0`):**  
    If there is no error, the wiper speed is determined based on the `WiprSpdReq` input. The `WiprSpdReq` values map to PWM duty cycles as follows:
    - **`WiprSpdReq` = 0**: PWM Duty Cycle = 0% (Wiper off)
    - **`WiprSpdReq` = 1**: PWM Duty Cycle = 10%
    - **`WiprSpdReq` = 2**: PWM Duty Cycle = 20%
    - **`WiprSpdReq` = 3**: PWM Duty Cycle = 30%
    - **`WiprSpdReq` = 4**: PWM Duty Cycle = 40%
    - **`WiprSpdReq` = 5**: PWM Duty Cycle = 50%
    - **`WiprSpdReq` = 6**: PWM Duty Cycle = 60%
    - **`WiprSpdReq` = 7**: PWM Duty Cycle = 70%

    The PWM command is designed to change smoothly between these stages to avoid abrupt transitions. A smoothing algorithm or interpolation method is implemented in the Simulink model to ensure gradual adjustments between different PWM levels based on `WiprSpdReq`.

- **Low Speed Mode (`WiprMod = 2`):**  
  The wiper motor operates at a constant low speed (`WiprMotPwmDutyCyc = 40%`).

- **High Speed Mode (`WiprMod = 3`):**  
  The wiper motor operates at a constant high speed (`WiprMotPwmDutyCyc = 70%`).

## Implementation Methods

### Method 1: Using Simulink Case Block

- **File**: `car_wiper_control_case.slx`
- **Description**: This method uses the Simulink Case block to manage different operational modes (`WiprMod`). The Case block organizes control logic into distinct cases, making it easy to handle different scenarios and ensure smooth PWM transitions in Auto mode.

### Method 2: Using Multi-Switches

- **File**: `car_wiper_control_switch.slx`
- **Description**: This method employs multi-switches to manage the different operational modes. Each switch controls a specific aspect of the wiper system, offering a different approach to implementing the control logic compared to the Case block method.

## Simulink Models

- **`car_wiper_control_case.slx`**: Demonstrates the use of the Case block for managing operational modes and smooth PWM transitions.
- **`car_wiper_control_switch.slx`**: Shows the use of multi-switches for controlling the wiper system.

## Getting Started

To run these models on your machine:

1. Ensure you have MATLAB and Simulink installed.
2. Download or clone this repository.
3. Open the desired Simulink model file (`car_wiper_control_case.slx` or `car_wiper_control_switch.slx`) in MATLAB.
4. Run the simulation and observe how the wiper operates based on different input scenarios.

## Customization

Both models can be customized to include additional features, such as more complex rain sensor models or different speed levels. They can also be integrated with real-time hardware systems for practical applications.

## Future Improvements

Potential improvements for this project could include:

- Enhancing the rain sensor model to simulate varying rainfall intensity.
- Implementing advanced feedback mechanisms for dynamic speed adjustment.
- Integrating the models with hardware-in-the-loop testing for real-time validation.

## License

This project is open-source and available under the MIT License. Feel free to use, modify, and distribute the code as per the terms of the license.

## Contact

If you have any questions or suggestions, feel free to contact me at [vikramkolupula@gmail.com].
