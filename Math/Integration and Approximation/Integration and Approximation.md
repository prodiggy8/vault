---
course: "[[Integration and Approximation]]"
---
```base
views:
  - type: table
    name: Integration and Approximation
    filters:
      and:
        - file.inFolder("Math/Integration and Approximation")
        - file.hasProperty("note")
    order:
      - file.name
      - note.note
      - file.ctime
      - file.mtime
    sort:
      - property: note.note
        direction: ASC
    columnSize:
      file.name: 240
      note.note: 82
      file.ctime: 213
      file.mtime: 204

```
