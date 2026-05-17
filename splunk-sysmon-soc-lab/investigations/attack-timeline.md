# Attack Timeline Reconstruction

## Stage 1 — Reconnaissance

### Commands executed:

cmd
whoami
hostname
ipconfig
net user
tasklist


### Observed:
- Process creation events generated
- Parent-child relationships visible
- User context logged

---

## Stage 2 — Encoded PowerShell

## Command:

powershell
powershell -enc SQBlAHgA


### Observed:
- powershell.exe execution
- encoded command flag detected
- suspicious process behavior identified

---

## Stage 3 — DNS Activity

## Commands:

cmd
nslookup google.com
curl https://example.com


### Observed:
- DNS query telemetry generated
- QueryName field captured
- Associated process visible

---

## Stage 4 — LOLBin Activity

## Commands:

cmd
certutil.exe -urlcache -split -f https://example.com test.txt
regsvr32.exe


### Observed:
- LOLBin execution telemetry generated
- High integrity process execution observed
- File creation and process telemetry logged

---

# Key Findings

- Successfully reconstructed attack timeline using Sysmon telemetry.
- Verified Splunk ingestion pipeline functionality.
- Investigated process creation, DNS, and LOLBin activity.
