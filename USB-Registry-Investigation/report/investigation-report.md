# Forensic Investigation Report: USB Registry Analysis

## 1. Case information
- **Case type:** Windows Registry / USB device artifact review
- **Environment:** Simulated lab scenario
- **Analyst:** [Add name]
- **Evidence source:** Windows `SYSTEM` hive, as described in lab notes
- **Tool:** Registry Explorer
- **Evidence hash:** Not provided
- **Acquisition method:** Not provided

## 2. Executive summary
This lab reviewed Windows registry locations associated with USB mass-storage enumeration and mounted-device information. The reported observations identify a Lexar USB Flash Drive, Rev 3.00, with a reported connection time of `2025-02-25 14:10:09`. The supplied employee logon reference is `2025-02-25 14:10`, placing the reported connection approximately nine seconds after logon.

These observations are consistent with Windows recognizing a USB storage device shortly after the supplied logon time. The described registry evidence does not prove that files were copied or that data exfiltration occurred.

## 3. Scope
The described review covered:
- `SYSTEM\\CurrentControlSet\\Enum\\USBSTOR`
- `SYSTEM\\MountedDevices`
- `SYSTEM\\CurrentControlSet\\Control\\DeviceClasses`

## 4. Methodology
1. Opened the Windows `SYSTEM` hive in Registry Explorer.
2. Reviewed USB mass-storage enumeration information under `USBSTOR`.
3. Reviewed `MountedDevices` for volume/device mappings.
4. Reviewed `DeviceClasses` for related device-interface information.
5. Compared the reported USB connection time with the supplied logon reference time.
6. Recorded the reported observations and limitations.

For a production-quality case record, attach screenshots or exports showing the exact registry paths, values, tool version, and timestamp interpretation.

## 5. Findings

### Finding 1 — USB device identification
- **Reported observation:** Lexar USB Flash Drive, Rev 3.00.
- **Artifact:** `SYSTEM\\CurrentControlSet\\Enum\\USBSTOR`.
- **Interpretation:** This registry location stores information about enumerated USB mass-storage devices. The reported description is consistent with Windows enumerating a Lexar USB storage device.
- **Qualification:** Confirm against the original hive and exact key/value evidence.
- **Does not establish:** File copying or exfiltration.

### Finding 2 — Timeline correlation
- **Supplied logon reference:** `2025-02-25 14:10`.
- **Reported USB connection:** `2025-02-25 14:10:09`.
- **Difference:** Approximately 9 seconds.
- **Interpretation:** If both timestamps use the same clock basis and the USB timestamp was interpreted correctly, the reported device activity occurred shortly after the supplied logon time.
- **Does not establish:** Who physically connected the device, intent, or file-transfer activity.

### Finding 3 — Mounted-device and device-interface review
- **Artifacts:** `SYSTEM\\MountedDevices` and `SYSTEM\\CurrentControlSet\\Control\\DeviceClasses`.
- **Reported action:** Both locations were reviewed during the lab.
- **Interpretation:** These locations can provide context about volume mappings and device-interface registration. Exact values should be documented before drawing more specific conclusions.
- **Qualification:** The exact values are not reproduced in this report.

## 6. Conclusion
The described registry review is consistent with Windows recognizing a Lexar USB mass-storage device. The reported connection time is approximately nine seconds after the supplied employee logon reference time.

**There is insufficient evidence in the described registry artifacts alone to conclude that confidential files were copied to the USB device or that data exfiltration occurred.**

## 7. Limitations
- Original hive and SHA-256 hash were not supplied with this report.
- Acquisition procedure, host identity, and tool version are not documented here.
- Exact registry paths, values, and raw data should be attached as screenshots or exports.
- Timestamp source and semantics must be verified.
- Device enumeration alone does not identify the person who connected the device.
- No file-copy evidence has been provided.

## 8. Recommended additional examination
- Examine `NTUSER.DAT`, ShellBags, LNK shortcut files, and Jump Lists.
- Examine `$MFT` and `$UsnJrnl`, where available.
- Review Windows event logs and endpoint telemetry.
- Correlate timestamps across sources, documenting time-zone and clock assumptions.
- Preserve original evidence, calculate hashes, and maintain chain-of-custody records.

## 9. Evidence handling
Do not publish raw registry hives, user-identifying data, or unredacted device serial numbers in a public repository. Keep original evidence in a controlled location and publish sanitized screenshots with reproducible notes.
