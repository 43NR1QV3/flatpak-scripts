# Flatpak Backup & Restore Tool

This repository contains tools to backup and restore your Flatpak applications and their custom configurations.

## Features

- 🔄 Automatic backup of Flatpak applications list
- ⚙️ Automatic backup of Flatpak override configurations
- 📦 Easy reinstallation of all your Flatpak applications
- 🛠️ Simple restoration of your custom Flatpak configurations

## Prerequisites

- **Flatpak:** This tool requires Flatpak to be installed on your system
  ```bash
  # Ubuntu/Debian
  sudo apt install flatpak
  
  # Fedora
  sudo dnf install flatpak
  
  # Arch Linux
  sudo pacman -S flatpak
  ```

- **Git:** Git is required for the hooks and repository management

## How It Works

This tool uses Git pre-push hooks to automatically:

1. Create a backup script of all your installed Flatpak applications
2. Save your Flatpak override configurations

## Reinstalling Your Flatpak Applications

When you need to reinstall your Flatpak applications (on a new system or after a fresh install):

1. Ensure Flatpak is installed on your system (see Prerequisites)

2. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/your-repo-name.git
   cd your-repo-name
   ```

3. Make the reinstallation script executable (if it's not already):
   ```bash
   chmod +x reinstall-flatpaks.sh
   ```

4. Run the reinstallation script:
   ```bash
   ./reinstall-flatpaks.sh
   ```

The script will automatically:
- Check for each application if it's already installed
- Skip applications that are already present
- Install missing applications from Flathub

## Restoring Your Flatpak Override Configurations

To restore your custom Flatpak configurations:

```bash
# Create a script to copy the override files
cat > restore-overrides.sh << 'EOF'
#!/bin/bash

# Source directory in the repository
SOURCE_DIR="$(pwd)/flatpak-overrides"

# Destination directory for Flatpak override files
DEST_DIR="${HOME}/.local/share/flatpak/overrides"

# Create destination directory if it doesn't exist
mkdir -p "$DEST_DIR"

# Copy all files from source directory to destination
echo "Restoring Flatpak override configurations..."
cp -r "$SOURCE_DIR"/* "$DEST_DIR"/ 2>/dev/null || true

echo "Flatpak override configurations have been restored!"
EOF

# Make the script executable
chmod +x restore-overrides.sh

# Run the script
./restore-overrides.sh
```

You can also copy and paste the above commands directly into your terminal to create and run the restore script.

## Recommended Usage

For the best experience:

1. Run the reinstallation script first to install all your Flatpak applications
2. Then run the restore script to apply your custom configurations
3. Restart any running Flatpak applications to apply the restored settings

## Notes

- The override configurations contain your custom settings for Flatpak applications
- These may include permissions, environment variables, and other application-specific settings
- If you've made significant changes to your Flatpak setup, consider committing and pushing those changes before reinstalling

---

💡 **Tip:** Keep this repository updated by regularly pushing changes to ensure your backups are current.
