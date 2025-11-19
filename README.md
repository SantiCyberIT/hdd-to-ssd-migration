# HP 550-127c – HDD to SSD Migration & Optimization

## Summary

This project documents how I diagnosed a **SMART failing hard drive** on an older HP Pavilion Desktop (model 550-127c), replaced it with a **Samsung 870 QVO SSD**, reinstalled Windows 10, installed drivers, and optimized the system for everyday use and future IT labs.

I treated it like a real help desk ticket: reproduce the issue, collect evidence, plan, execute, validate, and document.

---

## System Info

- **Model:** HP Pavilion Desktop 550-127c  
- **CPU:** AMD A10-7800 with Radeon R7  
- **RAM:** 8 GB  
- **Original Boot Drive:** 3.5" SATA HDD (failing SMART test)  
- **Replacement Drive:** Samsung 870 QVO 1TB SATA SSD  
- **OS:** Windows 10 Home, Version 22H2 (fresh install)

---

## 1. Problem Description

- System would not boot normally and showed a **SMART Hard Disk Error (Hard Disk 2 (302))**.
- HP diagnostics reported **SMART check: FAILED** on the original drive.
- Booting sometimes froze unless I immediately entered the diagnostics/UEFI menu.
- Goal:  
  - Avoid data loss.
  - Replace the failing drive.
  - Get the machine into a stable, usable state.

---

## 2. Diagnosis Steps

1. **Reproduced the error**
   - Recorded the exact SMART error message and failure code from HP’s blue error screen.

2. **Hardware diagnostics**
   - Entered **HP PC Hardware Diagnostics UEFI**.
   - Ran:
     - **Memory Quick Test** (to verify RAM was OK).
     - **Hard Drive Quick Check** on Drive 1.
   - Result: SMART check failed on the original HDD → confirmed physical drive failure.

3. **Physical inspection**
   - Opened the case and identified:
     - 3.5" HDD connected via SATA data + SATA power.
     - Separate optical drive.
     - Spare SATA power connector available.
   - Verified cables and ports were OK (rules out loose cable issues).

**Conclusion:** The spinning HDD itself was failing and needed to be replaced.

---

## 3. Remediation Plan

- Replace the failing HDD with a known-good SSD.
- Perform a **clean install** of Windows 10 from bootable USB.
- Install critical drivers (chipset, graphics, network).
- Apply Windows updates and basic optimizations.

---

## 4. Implementation

### 4.1 Hardware Work

1. Powered down PC and unplugged power.
2. Grounded myself and opened the case.
3. Disconnected SATA data and power from the failing HDD.
4. Mounted/placed the **Samsung 870 QVO 1TB SSD** and connected:
   - Existing SATA data cable.
   - Spare SATA power connector.
5. Left the old HDD disconnected (to prevent boot conflicts).

> Tools used: basic screwdriver set, anti-static precautions.

### 4.2 Creating Windows 10 Installation USB

1. On a working laptop:
   - Downloaded **Windows 10 Media Creation Tool** from Microsoft.
   - Used it to create a **bootable 128 GB SanDisk USB drive**.
2. Selected:
   - Language: English (United States)
   - Edition: Windows 10
   - Architecture: 64-bit
   - Media type: USB flash drive

### 4.3 Installing Windows 10 on the SSD

1. Booted the HP from the USB:
   - Entered boot menu / UEFI and selected the USB drive.
2. In Windows Setup:
   - Chose **Custom: Install Windows only (advanced)**.
   - Selected **Drive 0 – Unallocated Space (931 GB)** → **Next**.
3. Installer:
   - Copied Windows files.
   - Got files ready for installation.
   - Installed features and updates.
   - Rebooted into the new OS.
4. Completed first-time Windows setup (region, keyboard, account, etc.).

---

## 5. Driver & Firmware Cleanup

### 5.1 Windows Update

- Ran Windows Update multiple times until:
  - No more updates were offered.
  - .NET, cumulative updates, and basic drivers were installed.

### 5.2 HP & AMD Drivers

- Used **Google Chrome** to access vendor sites (Microsoft Edge had issues loading HP pages at first).
- Installed:
  - HP updates via HP support page for model 550-127c (firmware and system components where available).
  - Latest compatible **AMD Radeon R7 / A10-7800** driver from AMD support.
- Verified drivers in **Device Manager**:
  - No yellow exclamation marks.
  - Display Adapter showed **AMD Radeon(TM) R7 Graphics**.
  - Network adapters and audio devices functioning.

---

## 6. Performance & Disk Optimization

- Verified SSD recognized as **Solid state drive** in `Optimize Drives`.
- Ran **Optimize** on C: (TRIM) and confirmed status was OK.
- Confirmed system specs via `msinfo32`:
  - 8 GB RAM.
  - UEFI boot.
  - SSD as `Device\HarddiskVolume1`.

---

## 7. Outcome

- System now boots reliably from SSD with **no SMART errors**.
- Windows 10 fully updated and stable.
- Graphics and chipset drivers correctly installed.
- Desktop is now usable for:
  - Light daily use (browsing, office apps).
  - Future IT labs and practice environments.

---

## 8. Lessons Learned

- SMART 302 and failed HP diagnostics usually mean **replace the drive**, not just reinstall Windows.
- Having proper tools (USB installer, screwdriver set, SSD, flash drive) makes the process much smoother.
- Vendor driver sites (HP, AMD) plus Windows Update together give a more stable system than relying on Windows alone.
- Documenting each step (photos + notes) makes it easier to convert practical troubleshooting into a portfolio project later.

---

## 9. Tools & Technologies

- **Hardware:** HP 550-127c, Samsung 870 QVO 1TB SSD, SATA cables, basic toolkit.
- **Software:** Windows 10 Media Creation Tool, Windows 10 Home, HP Diagnostics UEFI, HP Support Assistant/website, AMD driver package.
- **Skills demonstrated:**
  - Hardware diagnostics and interpretation of SMART errors.
  - Safe replacement of a failing HDD with SSD.
  - Clean OS installation and boot configuration.
  - Driver research and installation from vendor sources.
  - Basic system optimization on SSD.

