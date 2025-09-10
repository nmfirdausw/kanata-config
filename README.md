# Kanata Configuration

This repository contains my personal [Kanata](https://github.com/jtroo/kanata) configuration files. Kanata is a cross-platform software keyboard remapper that runs as a background service, providing advanced keyboard customization capabilities.

## About Kanata

Kanata is a powerful keyboard remapper inspired by QMK firmware. It allows you to create complex keyboard layouts, modifier combinations, and custom key behaviors without needing to flash firmware on your keyboard.

- **GitHub Repository**: [https://github.com/jtroo/kanata](https://github.com/jtroo/kanata)
- **Full Documentation**: [Configuration Guide](https://github.com/jtroo/kanata/blob/main/docs/config.adoc)

## Configuration Files

### `mac.kbd` - macOS Configuration
The main configuration file for macOS with advanced features including:

#### Layout Support
- **QWERTY**: Standard QWERTY layout with enhancements
- **Canary**: Alternative ergonomic layout optimized for English typing

#### Key Features

**Home Row Mods (Canary Layout)**
- `C` → Control (left hand)
- `R` → Alt (left hand) 
- `S` → Shift (left hand)
- `T` → Meta/Cmd (left hand)
- `N` → Meta/Cmd (right hand)
- `E` → Shift (right hand)
- `I` → Alt (right hand)
- `A` → Control (right hand)

**Multi-Key Layer Access**
- **Space**: Tap for Space, Hold for Control layer (200ms tap, 9999ms hold)
- **Return**: Tap for Return, Hold for Symbol layer (200ms tap, 9999ms hold)
- **Escape**: Tap for Escape, Hold for Symbol layer (200ms tap, 9999ms hold)

**Layer System**
- **Control Layer**: Navigation keys and shortcuts (arrows, home, end, esc, tab)
- **Symbols Layer**: Programming symbols and special characters
- **Layers Switch**: Quick switching between QWERTY and Canary

**Chord Combinations** (50ms timeout, all layers)
- `S + D` → Tab
- `K + L` → Backspace

**Function Key Mappings**
- F1 → Brightness Down (🔅)
- F2 → Brightness Up (🔆)
- F3 → Mission Control
- F4 → Spotlight Search
- F7 → Previous Track (◀◀)
- F8 → Play/Pause (▶⏸)
- F9 → Next Track (▶▶)
- F10 → Mute (🔇)
- F11 → Volume Down (🔉)
- F12 → Volume Up (🔊)

**Advanced Features**
- Concurrent tap-hold enabled for smoother typing
- 200ms timing for tap-hold actions
- Key-specific hold behavior for home row mods
- Layer switching via grave key hold

### `win.kbd` - Windows Configuration
The Windows configuration provides the same powerful features as the macOS version with platform-appropriate adaptations:

#### Layout Support
- **QWERTY**: Standard QWERTY layout with enhancements
- **Canary**: Alternative ergonomic layout optimized for English typing

#### Key Features

**Home Row Mods (Canary Layout)**
- `C` → Control (left hand)
- `R` → Meta/Win (left hand) 
- `S` → Shift (left hand)
- `T` → Alt (left hand)
- `N` → Alt (right hand)
- `E` → Shift (right hand)
- `I` → Meta/Win (right hand)
- `A` → Control (right hand)

**Multi-Key Layer Access**
- **Space**: Tap for Space, Hold for Control layer (200ms tap, 9999ms hold)
- **Return**: Tap for Return, Hold for Symbol layer (200ms tap, 9999ms hold)
- **Escape**: Tap for Escape, Hold for Symbol layer (200ms tap, 9999ms hold)

**Layer System**
- **Control Layer**: Navigation keys and shortcuts (arrows, home, end, numbers)
- **Symbols Layer**: Programming symbols and special characters
- **Layers Switch**: Quick switching between QWERTY and Canary

**Chord Combinations** (50ms timeout, all layers)
- `S + D` → Tab
- `K + L` → Backspace

**Windows-Optimized Home Row Arrangement**
The Windows configuration uses an optimized modifier arrangement different from macOS:
- **Win key on R & I**: More accessible finger positions for Windows shortcuts (Win+R, Win+L, etc.)
- **Alt key on T & N**: Better ergonomics for common Alt+Tab and Alt+F4 combinations
- **Symmetric layout**: Left and right hand modifiers mirror each other for consistency
- **Stronger finger emphasis**: Places Windows key on stronger ring fingers (R, I)

**Windows-Specific Adaptations**
- Uses Windows key (Meta) instead of Cmd for modifier combinations
- Simplified function row without macOS-specific media keys
- Optimized for Windows keyboard layouts and shortcuts
- Compatible with standard Windows applications and system shortcuts

### `org.pqrs.Karabiner-VirtualHIDDevice-Daemon.plist` - Launch Daemon
Launchd configuration file for automatically starting the Karabiner VirtualHID daemon on macOS.

## Installation & Usage

### Prerequisites

#### macOS Requirements
For macOS users, you **must** install the Karabiner DriverKit VirtualHIDDevice before using Kanata:

1. **Download and install** [Karabiner-DriverKit-VirtualHIDDevice](https://github.com/pqrs-org/Karabiner-DriverKit-VirtualHIDDevice)
2. **Grant system extension permissions** when prompted
3. **Restart your Mac** after installation

**Optional: Auto-launch Daemon Setup**
To automatically start the Karabiner daemon on boot:

1. **Copy the plist file:**
   ```bash
   sudo cp org.pqrs.Karabiner-VirtualHIDDevice-Daemon.plist /Library/LaunchDaemons/
   ```

2. **Set proper permissions:**
   ```bash
   sudo chown root:wheel /Library/LaunchDaemons/org.pqrs.Karabiner-VirtualHIDDevice-Daemon.plist
   sudo chmod 644 /Library/LaunchDaemons/org.pqrs.Karabiner-VirtualHIDDevice-Daemon.plist
   ```

3. **Create log directory:**
   ```bash
   sudo mkdir -p /var/log/karabiner
   sudo chown root:wheel /var/log/karabiner
   ```

4. **Load and start the service:**
   ```bash
   # Load the service (registers it with launchd)
   sudo launchctl load /Library/LaunchDaemons/org.pqrs.Karabiner-VirtualHIDDevice-Daemon.plist
   
   # Start the service immediately
   sudo launchctl start org.pqrs.Karabiner-VirtualHIDDevice-Daemon
   ```

For more details, see: [Run via launchd](https://github.com/pqrs-org/Karabiner-DriverKit-VirtualHIDDevice?tab=readme-ov-file#run-karabiner-virtualhiddevice-daemon-via-launchd)

> ⚠️ **Important**: Without this driver, Kanata will not work on macOS. This is required for low-level keyboard input handling.

### Install Kanata

1. **Install Kanata**
   - Download from [releases](https://github.com/jtroo/kanata/releases)
   - Or build from source: `cargo install kanata`

#### Windows Requirements

For Windows users, Kanata may require additional setup depending on your system:

1. **Run as Administrator** (Recommended)
   - Kanata needs elevated privileges for low-level keyboard access
   - Right-click on Command Prompt/PowerShell and "Run as administrator"

2. **Optional: Install Interception Driver**
   - For better compatibility and performance
   - Download from [Interception website](http://www.oblita.com/interception)
   - Follow installation instructions for your Windows version

3. **Windows Defender/Antivirus**
   - You may need to add Kanata to your antivirus exceptions
   - Low-level keyboard tools are sometimes flagged as suspicious

2. **Run Configuration**
   ```bash
   # macOS
   kanata --cfg ~/.config/kanata/mac.kbd
   
   # Windows - Command Prompt/PowerShell
   kanata --cfg %USERPROFILE%\.config\kanata\win.kbd
   
   # Windows - PowerShell alternative
   kanata --cfg $env:USERPROFILE\.config\kanata\win.kbd
   ```

3. **Setup as Service** (Recommended)
   - **macOS**: Use `launchd` to run Kanata automatically
   - **Windows**: Use Task Scheduler, Windows Service, or startup folder

## Layout Overview

### Canary Layout
The [Canary layout](https://github.com/Apsu/Canary) is a modern ergonomic keyboard layout developed by the AKL (Alternate Keyboard Layout) community. This configuration uses the **Canary Matrix** variant, optimized for ortholinear and matrix keyboards.

**Official Repository**: [https://github.com/Apsu/Canary](https://github.com/Apsu/Canary)

#### Design Philosophy
Canary is built on several core principles:

**High Rolling (55%+ of trigrams)**
- Prioritizes "flowy" typing with smooth finger sequences
- Balances both inward and outward rolls
- Creates natural typing rhythms

**Primary Vowels on Right Hand**
- All main vowels (O, U, E, I, A) placed on the right hand
- Enables high roll percentages when combined with left-hand consonants
- Optimizes for common English letter combinations

**Strategic Finger Loading**
- Emphasizes stronger middle and index fingers
- Minimizes pinky usage to reduce strain
- Ring finger handles "liquid" consonants (L, R) effectively

**Minimal Same-Finger Bigrams (SFBs)**
- Reduces awkward same-finger sequences
- Optimizes letter placement based on English frequency patterns

#### Canary Matrix Layout (macOS)
```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  W  │  L  │  Y  │  P  │  B  │  Z  │  F  │  O  │  U  │  '  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  C  │  R  │  S  │  T  │  G  │  M  │  N  │  E  │  I  │  A  │
│ Ctrl│ Alt │Shift│ Cmd │     │     │ Cmd │Shift│ Alt │Ctrl │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  Q  │  J  │  V  │  D  │  K  │  X  │  H  │  /  │  ,  │  .  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

#### Canary Matrix Layout (Windows - Optimized)
```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  W  │  L  │  Y  │  P  │  B  │  Z  │  F  │  O  │  U  │  '  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  C  │  R  │  S  │  T  │  G  │  M  │  N  │  E  │  I  │  A  │
│ Ctrl│ Win │Shift│ Alt │     │     │ Alt │Shift│ Win │Ctrl │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  Q  │  J  │  V  │  D  │  K  │  X  │  H  │  /  │  ,  │  .  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

#### Key Letter Placements
- **T & N**: High-frequency letters on index fingers for optimal rolling
- **Vowel Block**: O-U-E-I-A positioned for efficient right-hand sequences  
- **Liquids L & R**: Placed on ring fingers to handle their complex combinations
- **Quote (')**: Strategically placed next to A to minimize conflicts with contractions

#### Control Layer (Hold Space)
Provides navigation and editing shortcuts:
```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │  6  │  7  │  8  │  9  │  0  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│Ctrl │ Alt │Shift│ Cmd │     │  ←  │  ↓  │  ↑  │  →  │ Ret │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │ Home│PgDn │PgUp │ End │     │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

#### Symbols Layer (Hold Return/Escape)
Programming symbols and special characters:
```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  !  │  (  │  )  │  {  │  %  │  ^  │  }  │  [  │  ]  │  "  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  ;  │  @  │  &  │  $  │  +  │  <  │  -  │  =  │  >  │  :  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  ~  │  #  │  |  │  /  │  *  │  \  │  _  │  ?  │  '  │  `  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

### Layer Switching
- Hold **grave** (`) key to access layer switching
- `1` + grave → Switch to QWERTY
- `2` + grave → Switch to Canary

## Customization

### Adding New Layouts
1. Define new source layout in `defsrc`
2. Create layer with `deflayer <name>`
3. Add switching alias in `defalias`

### Modifying Timings
- Tap-hold timing: Currently set to 200ms
- Chord timeout: Set to 50ms for all combinations
- Adjust in `tap-hold-release-keys` and `tap-hold-press-timeout`

### Creating Custom Chords
Add new chord combinations in the `defchordsv2` section:
```
(key1 key2) output_key timeout behavior (layers)
```

## Troubleshooting

### macOS Permissions
- Grant Accessibility permissions in System Preferences → Security & Privacy
- May need to disable System Integrity Protection for some features

### Windows Setup
- **Administrator Rights**: Kanata requires administrator privileges for low-level keyboard access
- **Interception Driver**: Consider installing for better compatibility and performance
- **Antivirus Software**: May need to whitelist Kanata executable
- **Windows Defender**: Add exception for Kanata if it gets flagged
- **Startup Configuration**: Use Task Scheduler, Windows Service, or startup folder for auto-start

### Platform Differences

#### Windows vs macOS Configuration
- **Function Keys**: Windows config omits macOS-specific media keys (brightness, volume, etc.)
- **Modifier Keys**: Uses Windows key (Meta) instead of Cmd key
- **Home Row Mods**: Optimized arrangement with Win key on R/I and Alt on T/N for better Windows ergonomics
- **System Integration**: No equivalent to Karabiner VirtualHIDDevice requirement
- **Layout Structure**: Simplified defsrc without function row in Windows version
- **Permissions**: Windows requires administrator rights vs macOS accessibility permissions

## Contributing

Feel free to use this configuration as a starting point for your own Kanata setup. Contributions and improvements are welcome!

## License

This configuration is provided as-is for personal use. Feel free to modify and distribute as needed.

---

*For more information about Kanata, visit the [GitHub repository](https://github.com/jtroo/kanata) and read the [full documentation](https://github.com/jtroo/kanata/blob/main/docs/config.adoc).*
