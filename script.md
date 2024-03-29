---
layout: default
title: Script
nav_order: 5
has_children: true
---

<link href="assets/prism-dark.min.css" rel="stylesheet" />
<link href="assets/style.css" rel="stylesheet">
<script src="assets/prism-core.min.js"></script>
<script src="assets/prism-cql.js"></script>

# Basic Script Syntax

<pre>
open(<i>Form</i>, <i>Version</i>)[<i>Form/Grid Actions</i>]
.<i>Outputs</i>
.<i>Actions</i>
.<i>Each</i>
</pre>

Where:

- _Form_: name of opening form.  Example `w01012b`.
- _Version_: optional version name.
- _Form/Grid Actions_: zero or more `form` or `grid` actions.
- _Outputs_: zero or more output definitions.
- _Actions_: zero or more execute actions.
- _Each_: optional each statement.

_Note_: The stripped `open(` _Form_ `)` statement submits the form with the `demo` flag to fetch the spes.

## Form/Grid Actions

The following `form` actions are available:

- `do(` _id*_ `)` : click a button/row/form exit.  Example `do(4)`.
- `set(` _id*_ `,` _value*_`)` : set control's value.  Example `set(14, "Some name")`.
- `qbe(` _QBE_ `,` _value*_`)` : set value of QBE column.  Example `qbe(1[19], 4001)`.
- `select(` _Row_ `)` : select grid row.  Example `select(1.10)`.

The following `grid` actions are available:

- `insert[` _grid*_ _one or more Row Actions_ `]`
- `update[` _grid*_ _one or more Row Actions_ `]`

Where _Row Action_ has the format:

_row*_ `:(` _one or more comma separated Column Actions_ `)` _followed by optional Each_

Where _Column Action_ has the format:

_column*_ `:` _value_

_id*_ : Control's AIS id.  
_value*_ : Literal in optional double quotes.  
_grid*_ : Grid's AIS id (normally `1`).  
_row*_ : Zero index row number.  
_column*_ : Grid's Column AIS id.

## Outputs

Output statement can be one of:

- `.output(` _Format_ `,` _zero or more Parameter_ `)`
- `.output.dump`. The AIS full return (useful for debugging).

Where:

- _Format_ is a double quoted string with optional `{i}` placeholders.
- _Parameter_ can be one of:
  - `$form` : returned form name.
  - `$title` : return form title.
  - `$row` : input row number.
  - `$col[i]` : input column with zero index `i`.  Example `$col[0]` is the first column.

## Actions

Action has the format:

`.action[` _Form\Grid Actions as above_ `]`

## Each

Each is a two dimensional array and can either be:

- `.each[` _elements_ `]` : where _elements_ is one or more array `[` (_string*_|_number_) `,...]`
- `.each@` _variable_: where _variable is `Excel` table name.

_string*_: must be in double quotes.

## Basic Samples

