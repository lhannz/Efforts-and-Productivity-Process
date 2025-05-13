# Best Practices, Error Findings and Solution

## Scenario

* Always change **Employee ID** data type to `type text`.
* Always create **EmpDateKey** for reliable data relationship keys.
* When transforming data, avoid using Use First Row as Headers, as this breaks your transformations when you archive old data.

## EmpDateKey M Code (Add Column → Custom Column)

```m
let
    AddedEmpDateKey = Table.AddColumn(
        Source,
        "EmpDateKey",
        each Text.From([EmployeeID]) & "_" & Date.ToText([EmpDate], "yyyyMMdd"),
        type text
    )
in
    AddedEmpDateKey
