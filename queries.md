### Failed logons over time (4625)
index=unluckytech_logs source="WinEventLog:Security" EventCode=4625
| timechart span=1m count AS "Failed Logons"

### Successful logons count (4624)
index=unluckytech_logs source="WinEventLog:Security" EventCode=4624
| stats count AS "Successful Logons"

### Top failed accounts
index=unluckytech_logs EventCode=4625
| stats count AS failures by Account_Name
| sort - failures
| head 10

### Top sources for failed logons
index=unluckytech_logs EventCode=4625
| eval src=coalesce(src_ip, src, ComputerName, host)
| stats count AS failures by src
| sort - failures
| head 10

### Failed → Successful sequence (simple transaction)
index=unluckytech_logs (EventCode=4625 OR EventCode=4624)
| transaction Account_Name startswith=(EventCode=4625) endswith=(EventCode=4624) maxspan=15m
| where eventcount > 1
| table Account_Name, host, eventcount, earliest, latest, duration

### New accounts created (4720)
index=unluckytech_logs EventCode=4720
| table _time, host, SubjectUserName, TargetUserName
| sort - _time
