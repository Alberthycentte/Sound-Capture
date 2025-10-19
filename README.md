# Sound Capture Device - User Manual By Albert Hycentte

## 📖 Table of Contents
1. [Introduction](#introduction)
2. [Hardware Overview](#hardware-overview)
3. [Getting Started](#getting-started)
4. [Operating Instructions](#operating-instructions)
5. [LED Status Indicators](#led-status-indicators)
6. [Technical Specifications](#technical-specifications)
7. [Firmware Upload Guide](#firmware-upload-guide)
8. [Troubleshooting](#troubleshooting)
9. [File Management](#file-management)
10. [Maintenance & Care](#maintenance--care)
11. [Advanced Configuration](#advanced-configuration)
12. [Safety Information](#safety-information)

---

## 🎤 Introduction

Welcome to the **Sound Capture Device**! This portable audio recorder allows you to:
- Record high-quality audio with a professional MEMS microphone
- Store recordings as standard WAV files on an SD card
- Play back recordings through a built-in amplifier and speaker
- Operate on battery power or USB for extended recording sessions

This device is perfect for voice memos, field recordings, interviews, lectures, music practice, or any situation where you need reliable audio capture.

---

## 🔧 Hardware Overview

### Main Components

| Component | Description | Location |
|-----------|-------------|----------|
| **ESP32-S3** | Main processor | Center of PCB |
| **INMP441** | MEMS microphone | Bottom right of board |
| **MAX98357A** | Class D audio amplifier | Near speaker connector |
| **SD Card Slot** | Storage for recordings | Bottom left edge |
| **USB-C Port** | Power & programming | Top-left corner |
| **Battery Connector** | LiPo battery input | Left side |
| **Speaker Connector** | 4-8Ω speaker output | Left side |

### User Interface

#### Buttons (Bottom Edge)
```
[START]  [STOP]  [PLAY]  [BOOT]  [EN]
   │       │       │       │      │
   │       │       │       │      └─── Reset button
   │       │       │       └────────── Programming mode
   │       │       └────────────────── Play last recording
   │       └────────────────────────── Stop recording/playback
   └────────────────────────────────── Start recording
```

#### Status LED
- Located near buttons
- Provides visual feedback for all operations
- See [LED Status Indicators](#led-status-indicators) for details

---

## 🚀 Getting Started

### What You Need

**Essential:**
- ✅ Sound Capture Device
- ✅ MicroSD card (4GB - 32GB, FAT32 formatted)
- ✅ USB-C cable (for charging/programming)
- ✅ 4Ω or 8Ω speaker (2-3W rating)

**Optional:**
- 🔋 3.7V LiPo battery (1000-2000mAh recommended)
- 💻 Computer (for firmware updates)

### Initial Setup

#### Step 1: Insert SD Card
1. Power off the device
2. Insert microSD card into slot (gold contacts facing down)
3. Push until it clicks into place
4. **Important:** Card must be formatted as FAT32

#### Step 2: Connect Speaker
1. Locate the 2-pin speaker connector (SPK)
2. Connect speaker wires 
3. Use 4Ω or 8Ω speaker rated for 2-3W

#### Step 3: Power Connection

**Option A: USB Power**
- Connect USB-C cable to device
- Connect other end to USB power adapter or computer
- LED should blink twice on startup

**Option B: Battery Power**
- Connect 3.7V LiPo battery to J2 connector
- Observe polarity: RED (+), BLACK (-)
- Battery charges automatically when USB connected

#### Step 4: First Power-On
1. Connect power source
2. Wait for LED indicators:
   - 2 blinks = System starting
   - 3 blinks = Ready to use
3. Device is now ready for recording!

---

## 🎵 Operating Instructions

### Recording Audio

**Basic Recording:**
1. **Press START button** once
   - LED turns ON (solid)
   - Recording begins immediately
2. Speak or capture audio (max 60 seconds)
3. **Press STOP button** to finish
   - LED blinks 2 times
   - File saved to SD card

**Recording Tips:**
- Speak clearly at normal volume
- Avoid covering microphone hole
- Recording stops automatically after 60 seconds
- Each recording creates a new numbered file (`rec_1.wav`, `rec_2.wav`, etc.)

### Playing Back Audio

**Playing Last Recording:**
1. **Press PLAY button** once
   - LED blinks slowly (500ms intervals)
   - Last recorded file plays automatically
2. Audio plays through connected speaker
3. Playback stops automatically at end
   - Or press STOP button to interrupt

**Volume:**
- Volume is set by hardware (12dB gain)
- To adjust, modify GAIN_SLOT resistor (see Advanced Configuration)

### Stopping Operations

**Stop Recording or Playback:**
- **Press STOP button** at any time
- Current operation terminates immediately
- LED blinks to confirm stop
- File is saved (if recording) before stopping

---

## 💡 LED Status Indicators

Understanding the status LED helps you know what the device is doing:

| LED Pattern | Meaning | Action |
|-------------|---------|--------|
| **2 blinks on power-up** | System initializing | Wait 2-3 seconds |
| **3 quick blinks** | System ready | Device ready to use |
| **Solid ON** | Recording in progress | Recording audio |
| **Slow blink (500ms)** | Playing audio | Playback in progress |
| **2 blinks after stop** | File saved successfully | Recording complete |
| **3 blinks (play press)** | No recordings found | Record something first |
| **5 rapid blinks** | Error detected | Check SD card or connections |
| **Continuous rapid blinks** | Critical error | Check troubleshooting section |

---

## 📊 Technical Specifications

### Audio Performance
| Parameter | Specification |
|-----------|---------------|
| **Sample Rate** | 16 kHz (voice optimized) |
| **Bit Depth** | 16-bit |
| **Channels** | Mono |
| **Format** | WAV (PCM uncompressed) |
| **Frequency Response** | 50 Hz - 8 kHz |
| **Microphone SNR** | 61 dB |
| **Amplifier Output** | 3.2W @ 4Ω, 1.4W @ 8Ω |
| **THD+N** | < 1% @ 1kHz |

### Recording Capacity
| SD Card Size | Recording Time @ 16kHz |
|--------------|------------------------|
| 4 GB | ~74 hours |
| 8 GB | ~148 hours |
| 16 GB | ~296 hours |
| 32 GB | ~592 hours |

**File Size:** Approximately 1.8 MB per minute of recording

### Power Specifications
| Mode | Current Draw | Battery Life (1000mAh) |
|------|--------------|------------------------|
| **Idle** | 50 mA | ~20 hours |
| **Recording** | 150 mA | ~6.5 hours |
| **Playback (medium volume)** | 250 mA | ~4 hours |
| **Charging** | Up to 1000 mA | ~1.5 hours |

### Physical Specifications
- **Supply Voltage:** 5V USB or 3.7V LiPo battery
- **Operating Temperature:** 0°C to 50°C
- **Storage Temperature:** -20°C to 60°C
- **Humidity:** 10% to 85% non-condensing

---

## 💻 Firmware Upload Guide

### Prerequisites

**Software Requirements:**
- Visual Studio Code (recommended) or Arduino IDE
- PlatformIO extension (for VS Code)
- USB-C cable
- Computer (Windows/Mac/Linux)

### Installation Steps

#### 1. Install PlatformIO
```bash
# For VS Code users:
1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X)
3. Search "PlatformIO IDE"
4. Click Install

# For command line:
pip install platformio
```

#### 2. Prepare Project
```
Create folder structure:
sound_capture/
├── platformio.ini
├── src/
│   └── main.cpp
└── include/
```

#### 3. Configure platformio.ini
```ini
[env:esp32-s3-devkitc-1]
platform = espressif32
board = esp32-s3-devkitc-1
framework = arduino
upload_speed = 921600
monitor_speed = 115200
```

#### 4. Upload Firmware

**Method A: Using VS Code**
1. Connect USB-C cable to device
2. Hold **BOOT button** (GPIO0)
3. Press and release **EN button**
4. Release **BOOT button**
5. Click "Upload" in PlatformIO toolbar
6. Wait for "SUCCESS" message

**Method B: Command Line**
```bash
cd sound_capture
pio run --target upload
```

#### 5. Verify Upload
```bash
# Open serial monitor
pio device monitor

# You should see:
=== Sound Capture Device ===
Initializing...
System ready!
```

### Firmware Updates
To update firmware in the future:
1. Download new firmware release
2. Follow upload steps above
3. Your recordings on SD card are preserved
4. Settings may need reconfiguration

---

## 🔧 Troubleshooting

### SD Card Issues

**Problem: "SD card mount failed"**
- ✅ Check card is fully inserted
- ✅ Format card as FAT32 (not exFAT or NTFS)
- ✅ Try a different SD card
- ✅ Clean SD card contacts
- ✅ Use card 32GB or smaller

**Problem: "Failed to create file"**
- ✅ Check SD card is not write-protected
- ✅ Ensure card has free space
- ✅ Verify card is formatted correctly
- ✅ Try creating `/recordings` folder manually

### Audio Issues

**Problem: No sound when recording**
- ✅ Check microphone is not blocked
- ✅ Speak louder or move closer (6-12 inches)
- ✅ Verify INMP441 power (3.3V)
- ✅ Check GPIO36, 37, 38 connections
- ✅ Test with different recording

**Problem: No sound during playback**
- ✅ Verify speaker is connected
- ✅ Check speaker impedance (4-8Ω)
- ✅ Ensure volume is adequate (hardware gain)
- ✅ Test speaker with another device
- ✅ Check GPIO3 is enabling amplifier

**Problem: Distorted or garbled audio**
- ✅ Reduce volume (change GAIN_SLOT)
- ✅ Don't speak too close to microphone
- ✅ Check for loose connections
- ✅ Verify sample rate (16kHz default)
- ✅ Try re-recording

### Power Issues

**Problem: Device won't turn on**
- ✅ Check USB cable is connected
- ✅ Verify battery is charged
- ✅ Try different USB power source
- ✅ Check battery polarity
- ✅ Press EN button to reset

**Problem: Battery not charging**
- ✅ Ensure USB is connected
- ✅ Check charge LED (D5) is ON
- ✅ Verify battery polarity
- ✅ Battery may be fully charged
- ✅ Wait 1-2 hours for full charge

### Button Issues

**Problem: Buttons not responding**
- ✅ Press firmly and release
- ✅ Wait 200ms between presses (debounce)
- ✅ Check device is in IDLE state
- ✅ Reset device (EN button)
- ✅ Verify GPIO connections

### Error LED Patterns

**5 rapid blinks:**
1. Check SD card is inserted
2. Verify card is formatted FAT32
3. Check all connections
4. Re-upload firmware
5. Check serial monitor for details

---

## 📁 File Management

### File Structure
```
SD Card Root/
└── recordings/
    ├── rec_1.wav
    ├── rec_2.wav
    ├── rec_3.wav
    └── ...
```

### Accessing Recordings

**On Computer:**
1. Remove SD card from device
2. Insert into computer SD card reader
3. Navigate to `recordings` folder
4. Copy WAV files to computer
5. Files can be played with any media player

**Supported Players:**
- Windows Media Player
- VLC Media Player
- QuickTime (Mac)
- Any WAV-compatible software

### File Naming
- Files automatically numbered: `rec_1.wav`, `rec_2.wav`, etc.
- Device remembers last number used
- Deleting files resets numbering to highest existing number + 1

### Storage Management

**Checking Free Space:**
- Serial monitor shows card size on startup
- Monitor: "SD Card Size: XXXXMB"

**Deleting Old Recordings:**
1. Remove SD card
2. Connect to computer
3. Delete unwanted files from `/recordings/` folder
4. Re-insert card into device
5. Next recording continues numbering

**Backup Recommendations:**
- Copy recordings to computer regularly
- Keep SD card backups
- Card can be reformatted if needed (loses all data)

---

## 🛠️ Maintenance & Care

### Daily Use
- Keep device clean and dry
- Avoid extreme temperatures
- Don't cover microphone hole
- Store in protective case when not in use

### SD Card Care
- Don't remove card while recording
- Keep contacts clean
- Avoid static discharge
- Replace every 2-3 years for reliability

### Battery Maintenance
- Charge fully before first use
- Don't fully discharge (keep above 20%)
- Charge at room temperature
- Replace if runtime significantly decreases
- Store at 40-60% charge if unused for months

### Speaker Care
- Don't exceed 3W rating
- Avoid water exposure
- Check connections periodically
- Replace if sound becomes distorted

### Cleaning
- Use dry, soft cloth for exterior
- Don't use liquids near electronics
- Compressed air can clean microphone hole
- Clean SD card slot with dry brush

### Firmware Updates
- Check for updates periodically
- Updates may add features or fix bugs
- Follow upload guide for updates
- Backup recordings before updating

---

## ⚙️ Advanced Configuration

### Changing Audio Quality

**Location:** Line 51-54 in `main.cpp`

```cpp
// Voice recording (default)
#define SAMPLE_RATE    16000
#define SAMPLE_BITS    16
#define I2S_CHANNELS   1

// Music quality
#define SAMPLE_RATE    44100  // CD quality
#define SAMPLE_BITS    16
#define I2S_CHANNELS   1      // or 2 for stereo

// Phone quality (smaller files)
#define SAMPLE_RATE    8000
```

**Effect on file size:**
- 8 kHz: ~0.9 MB/min
- 16 kHz: ~1.8 MB/min
- 44.1 kHz: ~5 MB/min

### Adjusting Recording Time

**Location:** Line 54 in `main.cpp`

```cpp
#define RECORD_TIME_MS  60000  // 60 seconds

// Change to:
#define RECORD_TIME_MS  120000  // 2 minutes
#define RECORD_TIME_MS  300000  // 5 minutes
```

### Volume Adjustment (Hardware)

**Current Configuration:**
- GAIN_SLOT connected to VSYST (5V) via 0Ω resistor (R23)
- This provides 12dB gain

**To Change Volume:**

| R23 Connection | Gain | Volume |
|----------------|------|--------|
| GND | 9dB | Quieter |
| +3.3V | 12dB | Normal (current) |
| 100K to GND | 15dB | Louder |
| Open (DNP) | 18dB | Maximum |

**To modify:** Remove R23 and connect to desired voltage

### Custom File Naming

**Location:** Line 382 in `main.cpp`

```cpp
// Default naming
currentFileName = "/recordings/rec_" + String(recordingNumber) + ".wav";

// Custom naming examples:
currentFileName = "/recordings/audio_" + String(recordingNumber) + ".wav";
currentFileName = "/recordings/memo_" + String(millis()) + ".wav";
```

### Buffer Size Optimization

**Location:** Line 57 in `main.cpp`

```cpp
#define DMA_BUF_LEN    512  // Default

// For better quality, increase:
#define DMA_BUF_LEN    1024

// For lower latency, decrease:
#define DMA_BUF_LEN    256
```

**Note:** Larger buffers = smoother recording but more memory usage

---

## ⚠️ Safety Information

### Electrical Safety
- ⚡ Use only 5V USB power supply
- ⚡ Battery: 3.7V LiPo only (1000-2000mAh)
- ⚡ Observe battery polarity
- ⚡ Don't short-circuit battery terminals
- ⚡ Disconnect power during repairs

### Battery Safety
- 🔋 Use quality LiPo batteries with protection circuit
- 🔋 Don't puncture, crush, or disassemble battery
- 🔋 Keep away from heat/fire
- 🔋 Don't charge unattended
- 🔋 Dispose properly at recycling center

### Operating Precautions
- 💧 Not waterproof - avoid moisture
- 🌡️ Don't use in extreme temperatures
- 👂 Avoid excessive speaker volume near ears
- 🎤 Microphone not for medical/safety-critical use
- 📱 May interfere with sensitive equipment

### Environmental
- ♻️ Dispose of electronics responsibly
- ♻️ Recycle batteries at designated facilities
- ♻️ Keep away from children and pets
- ♻️ Follow local e-waste regulations

---

## 📞 Support & Resources

### Getting Help
1. Check this manual first
2. Review troubleshooting section
3. Check serial monitor for error messages
4. Verify all connections
5. Try known-good components (SD card, battery, etc.)

### Technical Support
- **Serial Monitor:** Connect USB and run `pio device monitor`
- **Debug Output:** Detailed startup and operation info
- **Error Messages:** Specific problem indicators

### Additional Resources
- **ESP32-S3 Datasheet:** Technical specifications
- **INMP441 Datasheet:** Microphone specifications
- **MAX98357A Datasheet:** Amplifier details
- **PlatformIO Documentation:** Development environment

---

## 📄 Specifications Summary

| Category | Details |
|----------|---------|
| **Processor** | ESP32-S3 Dual-core @ 240MHz |
| **Memory** | 512KB RAM, 16MB Flash |
| **Microphone** | INMP441 MEMS I2S |
| **Amplifier** | MAX98357A Class D, 3.2W |
| **Storage** | MicroSD up to 32GB |
| **Power** | USB-C 5V or 3.7V LiPo |
| **Battery** | 1000-2000mAh (4-6 hours) |
| **Audio Format** | 16kHz, 16-bit, Mono WAV |
| **Dimensions** | 60mm × 90mm (approximate) |
| **Weight** | ~50g (without battery) |

---

## 🎓 Quick Start Guide

**First-Time Users:**
1. ✅ Insert FAT32-formatted SD card
2. ✅ Connect 4-8Ω speaker
3. ✅ Connect USB-C power or battery
4. ✅ Wait for 3 LED blinks (ready)
5. ✅ Press START to record
6. ✅ Press STOP when done
7. ✅ Press PLAY to listen
8. ✅ Enjoy your recordings!

---

## 📜 Version History

**v1.0.0** (Current)
- Initial release
- Basic record/play/stop functionality
- WAV file format support
- Auto-numbering system
- Power management
- Status LED indicators

---

## 📝 Notes

- Device designed for voice recording applications
- Not intended for professional music production
- Recordings are mono (single channel)
- Maximum 60 seconds per recording (configurable)
- SD card required for operation
- Speaker required for playback
- Battery optional (can run from USB)

---

**Thank you for choosing the Sound Capture Device!**

For firmware updates, bug reports, or feature requests, please refer to the project repository or contact technical support.

**Happy Recording! 🎤🎵**

---

*Manual Version: 1.0.0*  
*Last Updated: 2025*  
*Compatible with Firmware: v1.0.0*
