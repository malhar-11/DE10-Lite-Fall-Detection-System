# Real-Time Fall Detection System for DE10-Lite FPGA

A hardware-based fall detection and alert system implemented on the DE10-Lite FPGA board using VHDL. The system uses the onboard ADXL345 accelerometer to detect fall events in real-time and provides visual alerts with a user-cancelable countdown.

## Overview

Falls are a leading cause of injury, especially among elderly populations. This project addresses this critical safety concern by implementing an automated monitoring device that detects falls through kinematic signatures—specifically a period of free-fall followed by high-impact shock.

The system operates as a synchronous sequential circuit, providing deterministic real-time performance superior to software-based polling approaches.

## Features

- **Real-time fall detection** using onboard ADXL345 accelerometer
- **Custom I²C Master** interface operating at 100 kHz
- **Magnitude-squared algorithm** for rotation-invariant fall detection
- **30-second countdown** allowing users to cancel false alarms
- **Visual alerts** with 7-segment display and LED strobe
- **Debounced button input** for reliable user interaction
- **Modular VHDL design** for easy extension and maintenance

## How It Works

### Fall Detection Algorithm

The system distinguishes falls from normal motion using a magnitude-squared approach:

```
A² = X² + Y² + Z²
```

This avoids computationally expensive square-root operations while maintaining accuracy.

**Detection States:**
1. **Startup** - Waits for sensor stabilization
2. **Monitor** - Continuously checks acceleration magnitude
3. **Freefall** - Detects when A² drops below threshold (134,217,728)
4. **Impact Detection** - Confirms fall if acceleration spike exceeds threshold (1,254,456,536) within ~1 second

### System Architecture

The design consists of four modular components:

1. **Accelerometer Interface** - I²C Master for ADXL345 communication
2. **Fall Detection Logic** - FSM-based algorithm for pattern recognition
3. **Main Control FSM** - System supervisor coordinating all modules
4. **I/O Controller** - User interface with debouncing and display drivers

## Hardware Requirements

- DE10-Lite FPGA Development Board (MAX10)
- Built-in ADXL345 3-axis accelerometer
- 7-segment displays (6x)
- LEDs (10x)
- Push buttons (KEY0 for reset/cancel)

## Getting Started

### Prerequisites

- Intel Quartus Prime (Lite Edition recommended)
- VHDL development environment
- DE10-Lite board drivers

### Installation

1. Clone the repository:
```bash
git clone https://github.com/malhar-11/DE10-Lite-Fall-Detection-System.git
cd DE10-Lite-Fall-Detection-System
```

2. Open the project in Quartus Prime

3. Compile the design:
   - Analysis & Synthesis
   - Fitter
   - Assembler

4. Program the FPGA:
   - Connect the DE10-Lite board via USB
   - Use the Quartus Programmer tool
   - Select the generated `.sof` file

### Usage

1. **Normal Operation**: The 7-segment displays show "IDLE"
2. **Fall Detected**: System enters 30-second countdown
3. **Cancel Alarm**: Press KEY0 during countdown to return to idle
4. **Alarm State**: If countdown completes, LEDs strobe at 1Hz and display shows "HELP"
5. **Reset**: Press KEY0 to clear alarm and return to monitoring

## Testing

The system has been validated through multiple test scenarios:

- **Free-fall test** - 30cm drop onto cushioned surface
- **False positive test** - Rotation and moderate shaking
- **User interface test** - Countdown accuracy verification
- **Alarm state test** - Visual alert functionality

## Design Optimizations

- **I²C clock stretching** - Strict timing constraints for reliable communication
- **Signal noise filtering** - Startup state discards initial unstable samples
- **Resource efficiency** - Magnitude-squared avoids costly square-root operations
- **Modular architecture** - Separation of concerns for maintainability

## Future Enhancements

Potential extensions include:
- VGA output for visual feedback
- Audio buzzer for audible alerts
- Wireless notification capability
- Adjustable sensitivity thresholds
- Data logging for analysis

## Development Tools

- **Sigasi Visual HDL** - VHDL linting and syntax checking
- **VS Code** - Primary development environment
- **Quartus Prime** - Synthesis and programming

## References

- Analog Devices ADXL345 Datasheet (Rev. E, 2015)
- Terasic DE10-Lite User Manual (v2.1, 2017)
- Scott Larson I²C Master VHDL Logic (DigiKey, 2012)

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bugs and feature requests.

## License

This project is open source. Please check the repository for license details.

## Acknowledgments

- AI assistance from Gemini (VHDL syntax) and Claude (report optimization)
- DigiKey TechForum for I²C reference implementation

---

**Note**: This system is a prototype for educational and research purposes. For production medical devices, additional safety certifications and regulatory compliance would be required.
