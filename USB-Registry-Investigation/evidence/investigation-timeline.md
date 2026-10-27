# Evidence Timeline — USB Registry Investigation

| Time | Event / observation | Source | Status / interpretation |
|---|---|---|---|
| `2025-02-22` (approx.) | Earlier install date shown for the Lexar device | USBSTOR screenshot | Appears in the install columns; verify exact value against the original evidence |
| `2025-02-25 14:10` | Employee logon | Supplied lab notes | Reference time; underlying log source not included here |
| `2025-02-25 14:10:09` | USB last connected | USBSTOR screenshot / lab notes | Last-connected value; confirm timestamp semantics |
| ~9 seconds later | Difference between logon and last connection | Calculation | Assumes both times use the same clock basis |

## Interpretation
The supplied timeline places the last USB connection approximately nine seconds after the employee logon reference time. This is relevant context but does not establish that the employee connected the device, accessed files, or copied data.

## Details to add during evidence validation
- Exact source file and SHA-256 hash
- Registry hive and exact key path
- Value name and raw value, where applicable
- Whether each time is a key last-write time or a derived timestamp
- Time zone / UTC offset and clock assumptions
- Analyst notes and confidence

The original evidence files and hashes were not included here. Do not invent hashes, paths, or timestamps.
