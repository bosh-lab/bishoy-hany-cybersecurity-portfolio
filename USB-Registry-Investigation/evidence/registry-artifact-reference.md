# Windows USB Registry Artifact Reference

This guide explains the purpose and limits of the registry locations reviewed during the lab. It is a learning reference, not a substitute for recording exact values from the acquired evidence.

## 1. USBSTOR

**Purpose:** Commonly records information about USB mass-storage devices that Windows has enumerated, including device identifiers and hardware/model strings.

**What it may support:** A compatible USB storage device was recognized by Windows at some point.

**What it does not prove by itself:** That a person intentionally used the device, that files were copied, or that data left the organization.

## 2. MountedDevices

**Purpose:** Stores mappings between volume identifiers and device/drive-letter information.

**What it may support:** Context about storage volumes and Windows volume mappings.

**Caution:** A drive-letter mapping alone is not proof that a particular file was accessed or copied. Correlate it with other artifacts and the case timeline.

## 3. DeviceClasses

**Purpose:** Contains device-interface registration information that can help correlate device instances and interface identifiers.

**What it may support:** Additional context for a device instance and its interaction with Windows.

**Caution:** Interpret entries alongside USBSTOR, setup/device-installation records, event logs, and the actual hive metadata. Do not treat a registry key timestamp as a precise connection timestamp without validating the artifact and timestamp semantics.

## Case notes

The lab notes report a Lexar USB Flash Drive Rev 3.00 and a connection time of `2025-02-25 14:10:09`, approximately nine seconds after the reported employee logon at `2025-02-25 14:10`. These are reported observations and should be checked against the original evidence before being treated as verified forensic facts.

## Recommended corroboration

- Preserve and document the source hive, acquisition method, and hash values.
- Record full registry paths, value names, raw values, and the tool/version used.
- Correlate device identifiers with Windows device-installation/setup logs and available event logs.
- Examine LNK files, Jump Lists, ShellBags, `$MFT`, `$UsnJrnl`, and endpoint/EDR telemetry for file-access or transfer evidence.
- Build a timeline using validated timestamps and note timezone assumptions.

## Reporting language

Prefer: **“The reviewed registry artifacts are consistent with Windows recognizing a Lexar USB storage device.”**

Avoid: **“The employee copied confidential files to the USB.”** That conclusion requires independent evidence of file access or transfer.

> Evidence integrity note: Do not insert fabricated screenshots or example values into the evidence folder. If illustrative diagrams are added later, label them clearly as illustrative and separate them from actual case evidence.
