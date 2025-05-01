**Windows Installation & Upgrade Reference Guide**

Let me be clear—I do this frequently. As part of our service offering, we sell laptops and desktops, but we also perform clean installations of Windows and migrate user data when a customer’s drive is corrupted or otherwise unusable.

That said, installing Windows is typically straightforward.

We utilize **Rufus** alongside official **Windows 10 and 11 ISOs** to create bootable USB drives. From there, we boot into the installer and follow the guided process. So, why this document? Because despite the simplicity, there are a few edge cases and complications that make installation less than intuitive. Consider this your checklist for those situations.

---

### Common Installation Pitfalls

**1. Drive Not Detected**

Occasionally, Windows will fail to detect an SSD. In most cases, this is due to BIOS configuration:

- Ensure the **SATA Controller** is set to **AHCI**, not **RAID**. I’ve encountered this firsthand—changing the setting resolved the issue immediately.
- In some instances, a **BIOS firmware update** is required. Always verify the latest firmware version on the **motherboard manufacturer’s website**.

---

### Offline Account Setup (Windows 10 & 11)

For both Windows 10 and 11, we set up an **offline user account with no password**, and deselect all optional features, telemetry, and unnecessary configurations.

**Windows 11**, however, complicates this process. During setup, you’ll eventually reach the network selection screen—notice there is **no "Continue without internet" option**, unlike in Windows 10.

To bypass this:

1. Press **Shift + F10** to open a Command Prompt.
2. Enter:
   ```
   OOBE\BYPASSNRO
   ```
3. The system will reboot. Upon restarting, the "Continue without internet" option will now appear.

---

### Installing Windows 11 on Unsupported Hardware

Installing Windows 11 on unsupported devices requires ISO modification. A separate guide will cover how to **build a custom ISO** tailored for these machines.

---

### Upgrading to Windows 11 (Supported Devices)

For supported systems, upgrading is simple:

1. Insert the Windows 11 USB installer into the Windows 10 system.
2. Run `setup.exe` for an **in-place upgrade** that preserves files and applications.

---

### Upgrading on Unsupported Devices

This process is actually more straightforward than a clean install:

1. Insert the USB installer.
2. Before running `setup.exe`, execute the following registry modifications to bypass hardware checks.

Here’s a batch script we maintain on our Windows 11 installation media:

```batch
@echo off
echo Windows 11 Upgrade Bypass Script
echo.
echo Adding registry entries to bypass system requirements...
echo.

:: Enable bypass for TPM 2.0, Secure Boot, CPU, RAM, and Storage
reg add "HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig" /v BypassTPMCheck /t REG_DWORD /d 1 /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig" /v BypassSecureBootCheck /t REG_DWORD /d 1 /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig" /v BypassCPUCheck /t REG_DWORD /d 1 /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig" /v BypassRAMCheck /t REG_DWORD /d 1 /f
reg add "HKEY_LOCAL_MACHINE\SYSTEM\Setup\LabConfig" /v BypassStorageCheck /t REG_DWORD /d 1 /f

:: Enable unsupported hardware upgrade path
reg add "HKEY_LOCAL_MACHINE\SYSTEM\Setup\MoSetup" /v AllowUpgradesWithUnsupportedTPMOrCPU /t REG_DWORD /d 1 /f

echo Registry changes applied successfully!
echo.
echo You can now proceed with the Windows 11 upgrade.
pause
```

---

### Activation Considerations

In most cases, Windows will automatically activate using the digital license tied to the device’s motherboard. However, there are exceptions.

We **do not** activate Windows using third-party tools on systems intended for resale. That said, in situations where a customer's original drive failed—and the system had previously been activated—we **inform** them about an open-source project called [**Massgrave**](https://massgrave.dev/). This Microsoft Activation Script can be used to reactivate Windows or Office products.