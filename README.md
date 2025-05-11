# Efforts-and-Productivity-Process

# Power Query: Custom Columns in `lvcdrconsolidated`

This guide lists the steps to add custom columns in Power Query for the `lvcdrconsolidated` table.

---

## 1. PhoneNo

**New column name**: `PhoneNo`

**Custom column formula**:
```m
if [Home Phone] = null
   or [Home Phone] = ""
then
   [Cell Phone]
else
   [Home Phone]

