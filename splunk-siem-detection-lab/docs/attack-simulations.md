# Attack simulations used to validate the detections

All activity was run against my own isolated lab VMs.

| Rule | Simulation |
|---|---|
| Multiple Failed Logins / Brute Force Success | Locked the Windows VM, entered a wrong password 3 times, then logged in correctly |
| Suspicious PowerShell | `powershell -nop -enc dwBoAG8AYQBtAGkA` (base64 for `whoami`) |
| Privilege Escalation | `net user testuser <password> /add`, then `net localgroup administrators testuser /add`, then `/delete` afterwards |
| Web Attack SQLi/Traversal | `curl` requests to `/admin`, `/login.php`, a SQLi-style query string, and `../../etc/passwd` against the Apache server on Kali |
| Web Scanner Spike | Same curl requests, which return repeated 404s from one client IP |
