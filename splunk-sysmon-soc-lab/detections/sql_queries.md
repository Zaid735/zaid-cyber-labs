# SPL Detection Queries

## Process Creation Events

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational" "<EventID>1</EventID>"
```

Detects Sysmon process creation events.

---

## DNS Query Events

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational" "<EventID>22</EventID>"
```

Detects DNS telemetry events.

---

## Encoded PowerShell Detection

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational" "-enc"
```

Detects PowerShell executions using encoded commands.

---

## LOLBin Detection

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational" (certutil.exe OR regsvr32.exe OR rundll32.exe)
```

Detects potentially suspicious Living-Off-The-Land binaries.

---

## Network Connection Events

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational" "<EventID>3</EventID>"
```

Detects outbound network activity.
