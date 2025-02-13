# miniARM Robotics Project Setup Guide

## Prerequisites
-  Arduino IDE [Download here](https://www.arduino.cc/en/software)
-  USB cable (Type A to Type B)
-  Arduino Uno board

## Installation Steps

### 1. Arduino IDE Setup
```
# Windows check (PowerShell):
Test-Path $env:ProgramFiles\Arduino\arduino.exe

# macOS/Linux check:
which arduino
```

### 2. Board Configuration
1. Launch Arduino IDE
2. Navigate to `Tools > Board > Arduino AVR Boards > Arduino Uno`
3. Set port under `Tools > Port`:
   - Windows: `COMx` (x = number from Device Manager)
   - macOS: `/dev/cu.usbmodemXXXX`
   - Linux: `/dev/ttyACMx`

### 3. Library Installation
```bash
# CLI alternative (if using Arduino CLI):
arduino-cli lib install FastLED
arduino-cli lib install Tone
```

| Library  | Required Version | Installation Command     |
|----------|------------------|--------------------------|
| FastLED  | 3.6.0            | `arduino-cli lib install FastLED@3.6.0` |
| Tone     | 1.0.0            | `arduino-cli lib install Tone@1.0.0`    |

### 4. Serial Configuration
```
// Required baud rate configuration
void setup() {
  Serial.begin(115200); // Set to match serial monitor
  while (!Serial) {
    ; // Wait for serial port to connect
  }
}
```

### 5. First Upload
1. Connect Arduino via USB
2. Verify connection:
   ```bash
   arduino-cli board list
   ```
3. Upload sketch:
   ```bash
   arduino-cli compile --fqbn arduino:avr:uno
   arduino-cli upload -p /dev/cu.usbmodemXXXX --fqbn arduino:avr:uno
   ```

## Troubleshooting

### Common Issues
1. **Port Not Found**:
   - Reinstall [CH340G drivers](https://learn.sparkfun.com/tutorials/how-to-install-ch340-drivers/all)
   - Try different USB cable

2. **Baud Rate Mismatch**:
   ```
   // Verify in both code and serial monitor
   Serial.begin(115200); // Must match dropdown value
   ```

3. **Library Conflicts**:
   ```
   arduino-cli lib uninstall conflicting_library
   ```

## Project Structure
```
miniARM/
├── docs/             # Documentation assets
├── src/              # Source code
│   └── main.ino      # Primary sketch
└── libraries/        # Custom libraries
```

> **Warning**  
> Always verify board selection before uploading. Incorrect configurations may require manual bootloader reset.
```

This documentation includes:
-  Multiple installation paths (GUI and CLI)
-  Version-pinned dependencies
-  Troubleshooting section
-  File structure visualization
-  Platform-specific instructions
-  Safety warnings

Would you like me to create a separate troubleshooting FAQ or add any specific hardware configuration details?

