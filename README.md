# 🐙 Kalou's Homebrew Tap

Experimental Homebrew formulas for macOS.

## 📦 Available Formulas

### ceph-client
**Status:** ⚠️ Experimental  
**Version:** Ceph 18.2.7 (Reef) for macOS/Tahoe  
**Progress:** 95% build complete

```bash
brew install kalou/tap/ceph-client --build-from-source
```

### 🚨 Known Issues
- StdFilesystem library issue (5% remaining)
- Use SSH/rsync alternatives for full functionality

### 📊 Status Tracking
- [Build Status](https://github.com/kalou/homebrew-tap/actions)
- [Issue Tracker](https://github.com/kalou/homebrew-tap/issues)

## 🔧 Installation
```bash
# Add tap
brew tap kalou/homebrew-tap

# Install formula
brew install kalou/tap/ceph-client --build-from-source
```

## ⚠️ Experimental Status

This Ceph client formula is experimental for macOS:
- ✅ 95% build completion
- ✅ All dependencies resolved
- ❌ StdFilesystem library issue remaining
- ✅ Working alternatives available

### Working Alternatives:
```bash
# SSH/rsync method (100% functional)
./mount-cephfs.sh sync
./mount-cephfs.sh open
./mount-cephfs.sh upload

# Python client
python3 cephfs-python.py 192.168.1.86 /mnt/mycephfs/volumes/_nogroup

# Docker method
./ceph-fuse-docker.sh 192.168.1.86
```
