# Forensic Investigation Report: USB Registry Analysis

## 1. Case information
- **Case type:** Windows Registry / USB device artifact review
- **Environment:** Simulated lab scenario
- **Analyst:** Bishoy Hany
- **Evidence source:** Windows `SYSTEM` hive, as described in lab notes and shown in the walkthrough video
- **Tool:** Registry Explorer
- **Evidence hash:** Not provided
- **Acquisition method:** Not provided

## 2. Executive summary
This lab reviewed Windows registry locations associated with USB mass-storage enumeration and mounted-device information. The reported observations identify a Lexar USB Flash Drive, Rev 3.00, with a reported connection time of `2025-02-25 14:10:09`. The supplied employee logon reference is `2025-02-25 14:10`, placing the reported connection approximately nine seconds after logon.

These observations are consistent with Windows recognizing a USB storage device shortly after the supplied logon time. The registry evidence does not prove that files were copied or that data exfiltration occurred.

## 3. Scope
- `SYSTEM\CurrentControlSet\Enum\USBSTOR`
- `SYSTEM\MountedDevices`
- `SYSTEM\CurrentControlSet\Control\DeviceClasses`

## 4. Methodology
1. Opened the Windows `SYSTEM` hive in Registry Explorer.
2. Reviewed USB mass-storage enumeration information under `USBSTOR`.
3. Reviewed `MountedDevices` for volume/device mappings.
4. Reviewed `DeviceClasses` for related device-interface information.
5. Searched the hive for the device serial number from the scenario notes to find related keys and values.
6. Compared the reported USB connection time with the supplied logon reference time.
7. Recorded the observations and limitations.

## 5. Visual evidence
Screenshots were captured from the walkthrough video. The video is low resolution, so exact values should be re-checked against the original hive.

### 5.1 USBSTOR
![USBSTOR in Registry Explorer](../screenshots/01-usbstor.png)

The USBSTOR view lists two storage devices. One is the Lexar USB Flash Drive (Rev 3.00). The table includes install, first-install, last-connected, and last-removed columns.

### 5.2 MountedDevices
![MountedDevices in Registry Explorer](../screenshots/02-mounted-devices.png)

The MountedDevices key lists drive-letter and volume entries. One volume entry contains a device string that references the Lexar USB device.

### 5.3 DeviceClasses
![DeviceClasses in Registry Explorer](../screenshots/03-device-classes.png)

DeviceClasses contains multiple device-interface entries, including entries for the USBSTOR Lexar device.

## 6. Findings

### Finding 1: USB device identification
- **Observation:** Lexar USB Flash Drive, Rev 3.00.
- **Artifact:** `SYSTEM\CurrentControlSet\Enum\USBSTOR` (see 5.1).
- **Interpretation:** Consistent with Windows enumerating a Lexar USB storage device.
- **Qualification:** Confirm values against the original hive.
- **Does not establish:** File copying or exfiltration.

### Finding 2: Timeline correlation
- **Supplied logon reference:** `2025-02-25 14:10`.
- **Reported USB connection:** `2025-02-25 14:10:09` (the last-connected value).
- **Difference:** Approximately 9 seconds.
- **Interpretation:** If both timestamps use the same clock basis and were interpreted correctly, the device was last connected shortly after the supplied logon time.
- **Note on earlier activity:** The USBSTOR entry also appears to show an earlier install date (around 2025-02-22). Describe 14:10:09 as the last connection, not the first. Verify against the original evidence.
- **Does not establish:** Who connected the device, intent, or file transfer.

### Finding 3: Mounted-device and device-interface review
- **Artifacts:** `SYSTEM\MountedDevices` (5.2) and `SYSTEM\CurrentControlSet\Control\DeviceClasses` (5.3).
- **Observation:** Both contain entries referencing the same Lexar device. A hive-wide search for the serial number returned related keys and values.
- **Interpretation:** Corroborates the USBSTOR finding from independent locations.
- **Does not establish:** Which files were accessed or copied.

## 7. Conclusion
The registry review is consistent with Windows recognizing a Lexar USB mass-storage device, last connected approximately nine seconds after the supplied logon reference time.

**There is insufficient evidence in the registry artifacts alone to conclude that confidential files were copied to the USB device or that data exfiltration occurred.**

## 8. Limitations
- Original hive and SHA-256 hash were not supplied.
- Acquisition procedure, host identity, and tool version are not documented.
- Screenshots come from a low-resolution video; verify exact values.
- Timestamp source and semantics must be verified.
- Device enumeration does not identify who connected the device.
- No file-copy evidence has been provided.

## 9. Recommended additional examination
- `NTUSER.DAT` (including MountPoints2), ShellBags, LNK files, and Jump Lists.
- `$MFT` and `$UsnJrnl`, where available.
- Windows event logs and endpoint telemetry.
- Correlate timestamps across sources, documenting time-zone and clock assumptions.
- Preserve original evidence, hash it, and maintain chain of custody.

## 10. Evidence handling
Do not publish raw registry hives or user-identifying data in a public repository. Keep original evidence in a controlled location and publish sanitized screenshots with reproducible notes.
