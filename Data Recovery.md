# Data Recovery Guide for Technicians

When we start to look at data recovery, the first step is always assessing the health of the hard drive and getting a general sense of the situation. Data recovery requests can come from many sources: a corrupted Windows installation, a USB drive that isn't showing files, or simply someone who accidentally deleted files. Even a quick format on a USB drive doesn't necessarily mean the data is gone—recovery is still possible.

Since every recovery case is unique, it’s impossible to provide a comprehensive list of scenarios and solutions. Instead, this guide focuses on the core **tools** we use and offers practical examples to help you understand their applications. By learning the tools themselves, you'll be better prepared to handle unexpected situations as they arise.

---

## Tools We Use

- HDSentinel  
- HDClone  
- File Explorer  
- GetDataBack Pro (for NTFS/FAT)  
- PhotoRec

---

## HDSentinel

HDSentinel comes in both portable and installable versions. It allows us to check disk health and view information such as power-on hours, start/stop count, estimated remaining lifespan, and more. If a system is having issues and we suspect a failing disk (HDD or SSD), HDSentinel can confirm that quickly.

**Important Note:** HDSentinel can give misleading results if the drive is connected externally via USB. It may flag the health at 0%, even though it might still boot and function internally. We’ve had cases where a drive showed 0% health externally but revealed 70–80% health when installed internally. Still, a 0% reading—even if false—is a good indicator that the drive is on its way out.

If the OS is functional and the disk is readable, we usually **clone the drive** using HDClone and replace it with a new SSD.

---

## HDClone

HDClone lets us create a bit-for-bit clone of a client’s OS drive. We first pull an image from the failing drive, then restore that image onto a new SSD. The result is seamless—their user account, passwords, apps, and settings are preserved, but the system now runs on a faster and more reliable SSD.

Even if the drive isn't failing, we might recommend this upgrade when the task manager shows disk usage constantly at 100%, or when the system is unbearably slow. HDClone is our go-to tool for these cases.

---

## File Explorer (Manual Copying)

If the OS is too corrupted to clone or boot, cloning would only replicate the problem. In this case, we manually copy user files.

Here’s our process:
1. Remove the failing drive and connect it to another system.
2. Copy the user data to a staging folder labeled with the client’s name.
3. Transfer that data to an external drive.
4. Install a fresh copy of Windows on a new SSD.
5. Copy the data from the external drive to the new system.

Clients will need to reinstall their software, but their personal data will be intact.

---

## GetDataBack Pro & PhotoRec

When the drive doesn't mount at all, or files were deleted or lost in a quick format, we use:

### GetDataBack Pro

This tool reads from corrupted or partially functional file systems (NTFS/FAT). It scans the disk at a low level and attempts to reconstruct folders, files, and structures.

### PhotoRec

If GetDataBack can’t read the drive, we go lower-level. PhotoRec doesn’t rely on the file system—it scans for file signatures in the raw data. It pulls every recognizable file from the disk, bit-for-bit. The downside is that file names and folder structures are usually lost, and files are dumped in bulk.

PhotoRec is ideal for USB drives with small amounts of data. For large drives (e.g., 2TB), the process can take many hours or even a full day.

---

## When All Else Fails: DriveSavers

In cases where the drive has suffered severe physical damage—beyond what tools like PhotoRec can handle—we turn to a professional data recovery partner: **DriveSavers**.

They specialize in hardware-level recovery, with skilled technicians working in certified clean rooms. In some cases, they’ll disassemble the drive to repair or replace damaged components, transplant the platters into a new donor drive, or perform circuit-level diagnostics to retrieve the data directly.

DriveSavers offers free evaluations, and you’re only charged if they’re able to recover your data. For catastrophic failures, this is often the only path forward—and one worth considering when the data is truly irreplaceable.

---

By mastering the tools covered here and understanding when and how to use each one, you’ll be prepared for a wide variety of data recovery challenges—even those not explicitly outlined in this guide.