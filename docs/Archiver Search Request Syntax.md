---
stoplight-id: n5ihqtr83kjpd
---

# Archiver Search Request Syntax

## Query syntax: fields

A query is broken up into fields and operators.

You can search any field by typing the field name followed by “:” and then the term value you are looking for.

`tag:bankA`

Multi-word terms separated by spaces or containing a special character (e.g. colon or parentheses) are called “phrases” and must be surrounded by double quotes

`type:'November Campaign'`

Most fields support wildcard search. Symbol “?” represents a single character wildcard and “*” represents multiple characters (0 or more). If you want to include all PE executables in your results - use:

`type:bank*`

Query syntax support escaping if you want to include ‘*’ as a character. Query presented below looks for all type values that are containing asterisk:

`type:"*\**"`


## Query syntax: operators
Archiver query language supports three boolean operators: `AND`, `OR` and `NOT`.

### Warning

#### Boolean operators must be UPPERCASE.



If you want to search all samples that are tagged with anything that contains “emotet” word (e.g emotet_drop, ripped:emotet or just emotet) and exclude samples tagged as feed:spam - use:

`tag:*bank* AND NOT tag:'spam'`

Query syntax supports using parentheses to group logic expressions:

`name:bank* OR (tag:*bank* AND NOT tag:'spam')`


## Query syntax: ranges
Integer and date fields support range search. Range queries can be inclusive or exclusive of the upper and lower bounds.

### Warning

#### TO operator must be UPPERCASE.

Query written below will find all files that have size between 50 and 50000 bytes inclusive:

`size:[50 TO 50000]`

If you want to exclude one of the range sides, replace “[” character with “{“.

`size:{50 TO 50000]`

This will find files between 51 and 50000 bytes in size. Inclusive range queries are denoted by square brackets. Exclusive are denoted by curly brackets.

In most cases we want to search for that are only one-side bounded e.g. all files bigger than 50000 bytes. In that case, we can use single wildcard character to denote the infinity:

`size:[50000 TO *]`


## Query syntax: timestamps
With timestamps you can search for objects within certain time range. Timestamps must be provided in ISO 8601 format (e.g. `2025-01-21T07:08:05+00:00`)

If you want to find objects that were uploaded from the beginning of December till the 28th:

`upload_time:[2025-12-28T00:00:00+00:00 TO 2025-12-28T23:59:59+00:00]`

If you want to find objects that were uploaded from the beginning of January:

`upload_time:[2025-01-01T00:00:00+02:00 TO *]`

If you want to search for objects within time certain range:

`upload_time:[2025-01-21T19:08:00+02:00 TO 2025-01-21T19:08:59+02:00]`

If you want to search for objects uploaded after certain hour:

`upload_time:[2025-01-21T19:08:00+02:00 TO *]`

If you want to search for objects uploaded at certain minute:

`upload_time:"2025-01-21T19:08:05+02:00"`

Exclusive range is not allowed for the date-time field so this is not allowed:

`upload_time:{2025-01-21T19:08:05+02:00 TO *]`






