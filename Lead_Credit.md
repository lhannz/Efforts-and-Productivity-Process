#Power Query Transformation for Lead_Credit in PowerBI

## New column for RPC_Process
```
if [Process] = "RPC" or [Process] = "Hybrid" then
    "RPC"
else if [Process] = "RC" then
    "RC"
else
    null
```
