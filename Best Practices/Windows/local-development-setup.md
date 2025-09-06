# Windows Local Development Environment Setup

A comprehensive guide for setting up a high-performance Windows development environment using WSL 2.

## Prerequisites

- Windows 10 version 2004+ (Build 19041+) or Windows 11
- WSL 2 enabled (`wsl --install` or `wsl --set-default-version 2`)
- Sufficient system resources (recommended: 16GB+ RAM, 8+ CPU cores)

## WSL 2 Configuration

The `.wslconfig` file controls global WSL 2 settings. Create this file in your Windows user directory (`%USERPROFILE%\.wslconfig`):

```ini
[wsl2]
# Memory configuration
memory=24GB
# memoryRefresh=5000  # Uncomment to enable periodic memory reclamation (ms)

# CPU configuration
processors=12
# processorAffinity=0-11  # Uncomment to pin specific cores

# Disable swap for optimal k8s/container performance
swap=0
# swapFile=C:\\Users\\jlvmo\\wsl2swap.vhdx

# Networking configuration
networkingMode=mirrored
# dnsTunneling=true  # Uncomment for better DNS resolution
# firewall=false  # Uncomment if you manage firewall externally
# autoProxy=true  # Uncomment to use Windows proxy settings

# Disk performance optimizations
# pageReporting=true  # Uncomment to enable page reporting (reduces memory usage)
# idleThreshold=1  # Uncomment to set memory release threshold (minutes)
# localhostForwarding=true  # Already enabled by default with mirrored mode

# GPU and GUI support
guiApplications=true
# gpuSupport=true  # Uncomment if you have compatible GPU for compute

# Kernel and debugging
debugConsole=false
# kernel=C:\\path\\to\\custom\\kernel  # Uncomment for custom kernel
# kernelCommandLine=  # Uncomment to add kernel parameters

# Virtual disk settings
# growable=true  # Uncomment to allow VHDX to grow dynamically
# sparseVhd=true  # Uncomment to enable sparse VHD for space efficiency

# Additional performance tuning
# vmIdleTimeout=60000  # Uncomment to set VM idle timeout (ms)
# nestedVirtualization=true  # Uncomment if you need nested VMs
# safeMode=false  # Already disabled by default for performance
```

### Verification

After creating or modifying `.wslconfig`, restart WSL:

```powershell
# In PowerShell or Command Prompt
wsl --shutdown
wsl
```

Then verify your configuration:

```bash
# Check CPU allocation
lscpu | grep -E "^CPU\(s\):|Thread\(s\) per core:|Core\(s\) per socket:"

# Check memory allocation
free -h

# Check swap status
swapon --show

# Check WSL version and distro info
wsl --list --verbose
```

## Essential Development Tools

### Package Management

```bash
# Update package lists
sudo apt update && sudo apt upgrade -y

# Essential build tools
sudo apt install -y build-essential curl wget git vim

# Development libraries
sudo apt install -y libssl-dev libffi-dev python3-dev

# Container tools
sudo apt install -y docker.io docker-compose
```

### Terminal Enhancement

```bash
# Install Zsh and Oh My Zsh
sudo apt install -y zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Install useful CLI tools
sudo apt install -y htop neofetch tree jq ripgrep fd-find bat
```

## Performance Optimization Tips

### File System Performance

1. **Keep project files in WSL filesystem** (`/home/username/`) for best performance
2. **Avoid cross-filesystem operations** between Windows (`/mnt/c/`) and WSL
3. **Use WSL 2 native filesystem** for databases and build artifacts

### Memory Management

```bash
# Clear page cache when memory runs low
sudo sh -c "echo 3 > /proc/sys/vm/drop_caches"

# Monitor memory usage
watch -n 1 free -h
```

### Network Configuration

With `networkingMode=mirrored`, WSL 2 shares the Windows network stack:
- Services in WSL are accessible from Windows using `localhost`
- No port forwarding configuration needed
- Better VPN compatibility

## Troubleshooting

### Common Issues

1. **WSL not responding after config change**
   ```powershell
   wsl --shutdown
   wsl --list --running  # Verify all instances stopped
   wsl
   ```

2. **Memory not released back to Windows**
   ```bash
   # Inside WSL
   sudo sh -c "echo 1 > /proc/sys/vm/drop_caches"
   ```

3. **Docker performance issues**
   - Ensure Docker Desktop uses WSL 2 backend
   - Allocate sufficient resources in `.wslconfig`
   - Disable swap for container workloads

### Useful Commands

```bash
# Check WSL resource usage
wsl --status

# Export WSL distro for backup
wsl --export Ubuntu ubuntu-backup.tar

# Check disk usage
df -h
du -sh ~/

# Monitor system resources
htop
```

## Additional Resources

- [Microsoft WSL Documentation](https://docs.microsoft.com/en-us/windows/wsl/)
- [WSL Configuration Reference](https://docs.microsoft.com/en-us/windows/wsl/wsl-config)
- [WSL 2 Performance Best Practices](https://docs.microsoft.com/en-us/windows/wsl/compare-versions#performance-across-os-file-systems)
