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

**Smart Space Bar**
- Tap: Space
- Hold: Control layer access
- Timeout: 200ms tap, 9999ms hold

**Layer System**
- **Control Layer**: Navigation keys (arrows, home, end, page up/down)
- **Symbols Layer**: Programming symbols and special characters
- **Layers Switch**: Quick switching between QWERTY and Canary

**Chord Combinations** (50ms timeout)
- `W + E` → Escape (QWERTY layer)
- `S + D` → Tab (QWERTY layer)
- `I + O` → Backspace (QWERTY layer)
- `K + L` → Backspace (QWERTY layer)
- `L + ;` / `J + ;` → Enter (QWERTY layer)

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
Reserved for Windows-specific configuration.

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

2. **Run Configuration**
   ```bash
   # macOS
   kanata --cfg ~/.config/kanata/mac.kbd
   
   # Windows (when configured)
   kanata --cfg ~/.config/kanata/win.kbd
   ```

3. **Setup as Service** (Recommended)
   - **macOS**: Use `launchd` to run Kanata automatically
   - **Windows**: Use Task Scheduler or Windows Service

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

#### Canary Matrix Layout
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
│ Home│ End │PgUp │PgDn │     │  ←  │  ↓  │  ↑  │  →  │ Ret │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│     │     │     │     │     │     │     │     │     │     │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
```

#### Symbols Layer (Hold Alt positions)
Programming symbols and special characters:
```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  !  │  @  │  #  │  $  │  %  │  ^  │  &  │  [  │  ]  │  '  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  }  │  (  │  )  │  {  │  +  │  <  │  -  │  =  │  >  │  "  │
├─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┼─────┤
│  `  │  ~  │  |  │  /  │  *  │  \  │  _  │  ?  │  ;  │  :  │
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
- May require running as administrator
- Consider using Interception driver for better compatibility

## Contributing

Feel free to use this configuration as a starting point for your own Kanata setup. Contributions and improvements are welcome!

## License

This configuration is provided as-is for personal use. Feel free to modify and distribute as needed.

---

*For more information about Kanata, visit the [GitHub repository](https://github.com/jtroo/kanata) and read the [full documentation](https://github.com/jtroo/kanata/blob/main/docs/config.adoc).*
