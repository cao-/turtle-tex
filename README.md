# Turtle graphics for OpTeX

A small Logo-like turtle graphics package for OpTeX, inspired by the book [Turtle Geometry: The Computer as a Medium for Exploring Mathematics](https://direct.mit.edu/books/oa-monograph/4663/Turtle-GeometryThe-Computer-as-a-Medium-for).
The package uses
OpTeX's ordinary `\pdfliteral` whatsit for its default drawing backend, so
segments remain aware of the current TeX position and transformation.

## Usage

Put `turtle.opm` where OpTeX can find it, then load it like any other OpTeX
package:

```tex
\load[turtle]

\begturtle
\repeat 4 {\forward 60 \right 90 }
\endturtle

\bye
```

The turtle starts at the current TeX position and initially points upward.
Distances and coordinates are in TeX points. The package exposes only the
`\begturtle` and `\endturtle` scope commands. Inside that scope, the short
names `\forward`, `\backward`, `\right`, `\left`, `\penup`, `\pendown`,
`\pensize`, `\repeat`, and `\backend` are available.

For a local drawing scope, use the OpTeX-style environment:

```tex
\begturtle
\repeat 4 {\forward 60 \right 90 }
\endturtle
```

The short names exist only between `\begturtle` and `\endturtle`; the
surrounding document keeps its original TeX command meanings.

## Backends

Segment rendering is isolated in the local `\backend` command. The default backend is
implemented with OpTeX's ordinary `\pdfliteral` primitive. A replacement
backend receives five arguments: start x, start y, end x, end y, and pen
width.

```tex
\def\mybackend#1#2#3#4#5{%
  % Render one segment with another graphics system.
}
\begturtle
\backend\mybackend
\endturtle
```

This keeps the turtle movement and drawing algorithms independent from the
output technology, allowing a future MetaPost backend without changing the
public turtle commands.

## Examples

Compile from the repository root with:

```text
optex examples/basic.tex
optex examples/text.tex
optex examples/recursive.tex
```

The examples demonstrate basic shapes, graphics embedded among paragraphs,
and recursive tree and fern drawings.
