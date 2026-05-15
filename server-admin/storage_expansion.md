# 📦 Ubuntu Server Storage Expansion

The VMware is using a virtual disk file that acts as "hard
drive". This can be configured to use more storage.

---

## 🔧 Step 1 - Expand the VMware Virtual Disk

Add more storage to the VMware disk throught the VMware settings.

### Expand VMware Disk

```text
VM → Settings → Hard Disk → Utilities → Expand
```

---

## 🔧 Step 2 - Expand Ubuntu Partition + Filesystem

Ubuntu still thinks the disk is the old size, you must expand:
- partition
- filesystem

### Verify Ubuntu Detected New Disk

Observation:
- Ubuntu detected the new disk size
- LVM volume remained unchanged

```bash
lsblk
```
```bash
df -h
```

### 🧱 Initial Disk Layout

```bash
sda                         600G
├─sda1                        1M
├─sda2                      1.8G   /boot
└─sda3                     18.2G
  └─ubuntu--vg-ubuntu--lv  10G    /
```

### Expand Partition

Expand partition 3 to consume remaining free disk space

```bash
sudo growpart /dev/sda 3
```

### Resize LVM Physical Volume
Purpose:

Updates LVM to recognize newly available storage

```bash
sudo pvresize /dev/sda3
```

---

## ✅ Verification

Rerun

```bash
df -h
```

---

## Notes

### ⚠️ Important Discovery

VMware does not allow disk expansion when:
- The VM is running
- The VM is suspended
- Snapshots exist

### Resolution

The VM was:
1. Cloned
2. Snapshots removed
3. Expanded successfully

---


## 📚 Concepts Learned

- Virtual disk expansion
- VMware disk utilities
- Snapshots and cloning
- Linux partitions
- LVM architecture
- Physical volumes
- Logical volumes
- Filesystem resizing