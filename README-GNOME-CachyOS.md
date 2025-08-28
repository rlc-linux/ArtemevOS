# ArtemevOS CachyOS with GNOME Desktop

**A Performance-Optimized Desktop Gaming OS with Immutable Updates**

ArtemevOS CachyOS Edition combines the solid foundation of ChimeraOS with CachyOS performance optimizations and a GNOME desktop environment by default, while maintaining gaming capabilities.

## 🎯 Key Features

### 🖥️ Desktop-First Experience
- **GNOME Desktop** as the default session
- **Steam disabled by default** - no auto-launch on boot
- **Session Switcher** - easy toggle between Desktop and Gaming modes
- **Full desktop environment** with modern UI and applications

### ⚡ CachyOS Performance Optimizations
- **Optimized repositories** with x86-64-v3 packages
- **CachyOS LTS kernel** with BORE scheduler and gaming patches
- **Performance tuning** - split lock mitigate disabled, VM optimizations
- **Network optimizations** - improved throughput and latency

### 🔄 Immutable System Architecture  
- **Atomic updates** using frzr and BTRFS snapshots
- **Rollback capability** - safe updates with instant recovery
- **Persistent data** - /home and /var preserved across updates
- **Read-only system** - protected from corruption and malware

## 📦 What's Changed from ChimeraOS

### ✅ GNOME Desktop Setup
- Added `gdm` display manager
- Configured GNOME as default session
- Auto-login enabled for seamless experience
- Created session switcher utility

### ❌ Steam Auto-launch Disabled  
- Steam no longer starts automatically
- Hidden Steam autostart desktop entry
- Steam remains available but manual launch only
- Gaming mode can be enabled via session switcher

### 🚀 CachyOS Integration
- Added CachyOS repository configuration
- Included CachyOS keyring and mirrorlist
- Performance optimizations applied
- Enhanced pacman configuration

### 🛠️ New Utilities Added
- **`session-select`** - Switch between desktop/gaming modes
- **ArtemevOS Session Switcher** - GUI application for mode switching
- **Performance optimizations** - Applied automatically

## 🚀 Building the System

### Prerequisites
```bash
sudo pacman -S docker archiso
```

### Build Process
```bash
# Build the system image using Docker
sudo docker build -t artemevos-builder .
sudo docker run --rm --privileged \
  -v $(pwd)/output:/output \
  artemevos-builder \
  /workdir/build-image.sh
```

### Or build directly on Arch Linux
```bash
sudo ./build-image.sh
```

## 🎮 Session Switching

### Command Line
```bash
# Switch to GNOME desktop mode (default)
session-select gnome
# or
session-select desktop

# Switch to Steam gaming mode
session-select gaming  
# or
session-select steam
```

### GUI Application
Look for **"ArtemevOS Session Switcher"** in the Applications menu under System Settings.

## 🖥️ Default Experience

### First Boot
1. System boots to GNOME login screen
2. Auto-login as `gamer` user (password: `gamer`)
3. GNOME desktop environment loads
4. Steam available in applications but won't auto-launch

### Desktop Mode (Default)
- Full GNOME desktop environment
- All applications accessible
- Steam available but manual launch
- Standard Linux desktop experience
- Gaming controllers work normally

### Gaming Mode (Optional) 
- Steam Big Picture interface
- Console-like gaming experience  
- Gamescope compositor for optimal gaming
- Automatic controller navigation
- Switch back via session switcher

## 🔧 Configuration

### Changing Default Behavior
```bash
# To auto-launch Steam in desktop mode (if desired)
rm ~/.config/autostart/steam.desktop

# To permanently default to gaming mode
sudo systemctl disable gdm
sudo systemctl enable lightdm
sudo session-select gaming
```

### Performance Tweaks
System includes CachyOS optimizations:
- `kernel.split_lock_mitigate=0` - Better gaming performance
- Enhanced VM settings for gaming workloads
- Network optimizations for low latency
- ZRAM enabled for better memory management

### Package Management
```bash
# CachyOS packages are prioritized automatically
pacman -S package-name

# Force install from specific repository
pacman -S cachyos/package-name  # CachyOS optimized
pacman -S extra/package-name    # Standard Arch
```

## 📋 System Information

### Included Desktop Applications
- **GNOME Shell** - Modern desktop environment
- **GNOME Control Center** - System settings
- **GNOME Console** - Terminal emulator  
- **GNOME Software** - Package manager GUI
- **GNOME Text Editor** - Code/text editing
- **GNOME Tweaks** - Advanced customization
- **Firefox** (Epiphany) - Web browser
- **Nautilus** - File manager

### Gaming Applications (Available)
- **Steam** - Gaming platform (manual launch)
- **RetroArch** - Retro gaming emulation
- **Gamescope** - Gaming compositor
- **MangoHud** - Gaming performance overlay

### Development Tools
- **Flatpak** - Universal package manager
- **Distrobox** - Container-based development
- **Git** - Version control
- **Various compilers** - Development tools

## 🔄 Updates & Maintenance

### Automatic Updates
- System checks for updates automatically
- Updates are downloaded and prepared
- Reboot applies update atomically
- Previous version remains available for rollback

### Manual Updates
```bash
# Check for system updates
sudo frzr-deploy

# Rollback if needed
sudo frzr-unlock
# Select previous deployment from GRUB menu
```

### Managing Applications
```bash
# Install desktop applications
flatpak install app-name

# Install development tools
distrobox create --image archlinux:latest dev
distrobox enter dev
# Install packages inside container
```

## 🎯 Use Cases

### Perfect For:
- **Desktop Linux users** who want gaming capability
- **Developers** who need a stable system with rollback
- **Content creators** who want desktop apps + gaming
- **Users wanting CachyOS performance** in desktop environment
- **System administrators** who prefer immutable systems

### Gaming When Needed:
- Use session switcher to enable gaming mode
- Steam Big Picture for console experience
- Return to desktop when done gaming
- Best of both worlds approach

## 🔧 Troubleshooting

### Session Issues
```bash
# If session switcher doesn't work
sudo systemctl restart gdm

# Check current session
echo $XDG_CURRENT_DESKTOP
loginctl show-session $(loginctl | grep $(whoami) | awk '{print $1}') -p Type
```

### Steam Issues
```bash
# If Steam won't launch
steam --reset

# Check Steam service status
systemctl --user status steam
```

### System Recovery
```bash
# From GRUB menu, select previous deployment
# Or from command line:
sudo frzr-deploy --rollback
```

## 📚 Documentation

- **ArtemevOS**: https://github.com/ArtemevOS/artemevos
- **CachyOS**: https://cachyos.org
- **ChimeraOS**: https://chimeraos.org  
- **GNOME Desktop**: https://gnome.org
- **frzr**: https://github.com/ChimeraOS/frzr

## 🙏 Credits

- **CachyOS Team** - Performance optimizations and repositories
- **ChimeraOS Team** - Base system and frzr immutable framework
- **GNOME Project** - Desktop environment
- **Arch Linux** - Solid foundation

---

**ArtemevOS CachyOS with GNOME** - *Desktop Performance Meets Gaming Capability*

The best of all worlds: CachyOS performance, GNOME desktop productivity, ChimeraOS gaming features, and immutable system reliability.
