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
```

## 2. EmpAppNoKey
```m
Text.From([Employee ID])
& "-"
& Text.From([AppNo])
```

## 3. EmpDateKey
```m
Text.From([Employee ID])
& "-"
& Date.ToText(
    [Date],
    "yyyyMMdd"
  )
```
## 4. EmpPhoneKey
```m
Text.From([Employee ID])
& "-"
& [PhoneNo]
```
## 5. AppNo
```m
let
    parts = Text.Split([ACCOUNT], "-")
in
    if List.Count(parts) = 3
       and List.Contains(
           {"P","R","T","D","N","C"},
           Text.End(parts{0}, 1)
       )
    then
        [ACCOUNT]
    else
        "-"
```
## 5. DateText

```m
Date.ToText([Date], "dddd, MMMM d, yyyy")
```
