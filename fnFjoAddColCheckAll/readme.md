# fnFjoAddColCheckAll
Add a new column CHECK_ALL (default value) to quickly check if there are difference or not.
> _function (<code>inputTable</code> as table, <code>listCheckedColumns</code> as list, optional <code>newColumnName</code> as text) as table_

## Description 
Add a new column CHECK_ALL (default value) to quickly check if there are difference or not.

## Code

````
let
    Fonction = (TableInput as table, ListFields as list, optional inputNewColumnName as text) =>
    let
        StrNewcolName = if inputNewColumnName <> null then inputNewColumnName else "CHECK_ALL",
        ListCheckedFields = List.Accumulate(ListFields, {}, (acc, val) => List.InsertRange(acc, List.Count(acc), {"CHECK_" & val})),
        New_Col_CHECK_ALL = Table.AddColumn(TableInput, StrNewcolName, each if Text.Contains(List.Accumulate(ListCheckedFields, "", (acc, val) => Text.Combine({acc, Record.Field(_, val)})), "|") then "KO" else "OK", type text)
    in
        New_Col_CHECK_ALL
in
    Fonction
````
