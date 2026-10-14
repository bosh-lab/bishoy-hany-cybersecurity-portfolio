# Evidence Timeline — USB Registry Investigation

| Time | Event / observation | Source | Status / interpretation |
|---|---|---|---|
| `2025-02-25 14:10` | Employee logon | Supplied lab notes | Reference time; underlying log source not included here |
| `2025-02-25 14:10:09` | USB connection reported | Lab notes / registry analysis | Reported timestamp; confirm exact artifact and timestamp semantics |
| ~9 seconds later | Difference between the two times | Calculation | Assumes both times use the same clock basis |

## Interpretation
The supplied timeline places the reported USB connection approximately nine seconds after the employee logon reference time. This is relevant context but does not establish that the employee connected the device, accessed files, or copied data.

## Details to add during evidence validation
- Exact source file and SHA-256 hash
- Registry hive and exact key path
- Value name and raw value, where applicable
- Whether the time is a key last-write time or a derived timestamp
- Time zone / UTC offset and clock assumptions
- Screenshot or exported artifact filename
- Analyst notes and confidence

The original evidence files and hashes were not included here. Do not invent hashes, paths, or timestamps.
