# Parsing Logic

## Example

```
+---+---+-------+
| 1 | X |   433 |
+---+---+-------+
+---+---+-------+
|   |444|       |
+---+---+-------+

- 433 -
++
++

- 1 -
+-+-+-+
|3| | |
+-+-+-+
+-+-+-+
+-+-+-+


- 444 -
++
++



- 3 -
++
++
```

## The Syntax & Semantics

Every file has at least one field at the very top which shows the most outer field. Every cell could be empty, have an "X", an "O", or a number. The numbers are field ids. Every number then must show up in a "field header" later in the file.

File headers have the following syntax:

```
- <field id> -
```

The field header is followed by a field body. The field body is a grid of cells, analogous to one on top.

Fields are bordered. The vertical boundries are made of pipe characters ("|), the horizontal boundries are made of dashes ("-"), and the corners are made of plus characters ("+").

Additionally, there is a special syntax for an empty field out of convenience:

```
++
++
```

Every field is made of 3x3 cells, and every cell can be empty, have an "X", an "O", or a field id, which must be referenced later in the file. A field cell must be close off and rectangular, thoug it does not have to be a square. The value in the cell does not have to be centered and could be anywhere in the cell.

The field headers can be in any order, but field ids must be unique.

Between a field and the following field header, ther can be any number of empty lines or lines whitespace in them.

Between a field header and the field body after it which is associated with it, ther cannot be any empty lines, just one line break.
