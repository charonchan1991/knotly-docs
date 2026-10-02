# Language Reference

This page is a quick lookup for Knotly’s pattern language. Instructions are case-insensitive: `6X` and `6x` mean the same thing, though uppercase letters are recommended for XVA notation and lowercase abbreviations for U.S. terminology. You can mix the two systems, but using one consistently makes a pattern easier to read. In the forms below, `N` / `n` means a positive integer, `Pn` a part code, `Rn` a round or row code, and `Sn` a stitch position.

## Stitch reference

### Basic stitches

Basic stitches are a series of stitches widely used throughout most patterns. They always consume one root stitch from the preceding round and produce one final stitch except for chain stitches and skips. You can work them individually or combine them into [compound increases and decreases](/docs/dsl/shaping#compound-increases-and-decreases).

| Stitch | XVA notation | U.S. terminology | Consumed → produced |
|---|---|---|---|
| Magic ring* | `MR` / `MR[N]` | `mr` / `mr[N]` | 0 → N |
| Chain | `CH` | `ch` | 0 → 1 |
| Slip stitch | `SL` | `sl` / `ss` | 1 → 1 |
| Single crochet | `X` | `sc` | 1 → 1 |
| Half double crochet | `T` | `hdc` | 1 → 1 |
| Double crochet | `F` | `dc` | 1 → 1 |
| Treble crochet | `E` | `tr` | 1 → 1 |
| Double treble crochet | `DTR` | `dtr` | 1 → 1 |
| Skip | `K` | `sk` | 1 → 0 |

_* A magic ring can only be used in `R0` as a foundation_

### Increases and decreases
An increase produces multiple stitches from one root stitch, while a decrease works multiple root stitches together into one. By changing the stitch density in specific areas, increases and decreases help shape the finished piece.

| Operation | XVA notation | U.S. terminology | Consumed → produced |
|---|---|---|---|
| Two-stitch single crochet increase | `V` / `XV` | `sc2inc` | 1 → 2 |
| Two-stitch half double crochet increase | `TV` | `hdc2inc` | 1 → 2 |
| Two-stitch double crochet increase | `FV` | `dc2inc` | 1 → 2 |
| Two-stitch treble crochet increase | `EV` | `tr2inc` | 1 → 2 |
| Three-stitch single crochet increase | `W` / `XW` | `sc3inc` | 1 → 3 |
| Three-stitch half double crochet increase | `TW` | `hdc3inc` | 1 → 3 |
| Three-stitch double crochet increase | `FW` | `dc3inc` | 1 → 3 |
| Three-stitch treble crochet increase | `EW` | `tr3inc` |  1 → 3 |
| Single crochet two together | `A` / `XA`| `sc2tog` / `sc2dec` | 2 → 1 |
| Half double crochet two together | `TA` | `hdc2tog` / `hdc2dec` | 2 → 1 |
| Double crochet two together | `FA` | `dc2tog` / `dc2dec` | 2 → 1 |
| Treble crochet two together | `EA` | `tr2tog` / `tr2dec` | 2 → 1 |
| Single crochet three together | `M` / `XM` | `sc3tog` / `sc3dec` | 3 → 1 |
| Half double crochet three together | `TM` | `hdc3tog` / `hdc3dec` | 3 → 1 |
| Double crochet three together | `FM` | `dc3tog` / `dc3dec` | 3 → 1 |
| Treble crochet three together | `EM` | `tr3tog` / `tr3dec` | 3 → 1 |
| Arbitrary increase (`N`: integer, `st`: stitch type) | `[N st]+` | `stNinc` | 1 → N |
| Arbitrary decrease (`N`: integer, `st`: stitch type) | `[N st]-` | `stNtog` / `stNdec` | N → 1 |

In U.S. terminology, replace `st` with `sc`, `hdc`, `dc`, `tr`, or `dtr`. In XVA notation, `X`, `T`, `F`, and `E` specify the stitch type. For U.S. decreases, `tog` and `dec` are interchangeable.

Square brackets also allow mixed-stitch compounds: `[sc, hdc, dc]+` works three stitches into one root stitch, while `[sc, hdc, dc]-` works three roots together as one stitch. The `+` on a compound increase is optional; the `-` on a compound decrease is required. You can use this technique to create a [shell stitch](/docs/dsl/special-stitches#shells).

### Textured stitches

Textured stitches refer to 3D crochet stitches created by grouping multiple stitches into a single space and closing them together so they pop out from the fabric.

| Stitch | XVA notation | U.S. terminology | Default components | Consumed → produced |
|---|---|---|---|---|
| Puff | `Q` | `puff` | Four half double crochets | 1 → 1 |
| Bobble | `Q[4F]` | `bobble` | Four double crochets | 1 → 1 |
| Popcorn | `G` | `popcorn` | Five double crochets | 1 → 1 |

A bracketed parameter changes the number and type of components in a textured stitch, for example: `puff[5hdc]`, `bobble[5dc]`, `Q[5T]`, `G[4F]`, etc. Each textured stitch consumes one root stitch and counts as one final stitch, regardless of its component count. For construction details, see [Special Stitches](/docs/dsl/special-stitches).

## Command reference

### End-of-round commands

A project’s **round mode** determines how Knotly completes each round or row when no explicit end-of-round command is present. You can override the default mode for an individual line by adding an **end-of-round command**:

| Round mode | XVA notation | U.S. terminology | What it does |
|---|---|---|---|
| Joined rounds | `$SL` | `$sl` / `$ss` | Closes the current round with a virtual slip stitch |
| Continuous rounds | `-$SL` | `-$sl` / `-$ss` | Leaves the current round open for continuous work |
| Rows | `turn` |  `turn` | Ends and turns the current row, leaving it open |

Place **end-of-round commands** at the end of an instruction line. If none is present, the project’s default round mode determines whether Knotly joins, continues, or turns. See [Round modes and end-of-round controls](/docs/dsl/fundamentals#round-modes-and-end-of-round-controls) and [Starting a part](/docs/dsl/writing-instructions#starting-a-part).

### Loop-selection commands

By default, Knotly works through both loops of each stitch, except when working into chain stitches. For a chain stitch, the back loop is preferred by Knotly unless another loop is specified. To change the default behavior, use a combination of the following **loop-selection commands**:

| Command | What it does |
|---|---|
| `flo` | works subsequent stitches through the **front loop only** |
| `blo` | works subsequent stitches through the **back loop only** |
| `both` / `bthl` | returns to working through **both loops** |
| `bump` | works into the **back bump** of a chain stitch |

These commands do not create stitches themselves, so their position within the instruction sequence matters. A selected loop remains active until another loop command appears or the instruction line ends. See [Shaping: Loop selection](/docs/dsl/shaping#loop-selection).

### Position-control commands

Position-control commands move the current working position without creating a regular stitch. Their placement in the instruction sequence determines which root stitch the next stitch will use.

| Command | What it does | Consumed → produced |
|---|---|---|
| `K` / `sk`  | Skips the next available root stitch and moves forward one position | 1 → 0 |
| `bk` | Moves back one position without reversing the working direction | 0 → 0 |
| `r[N]` | Reverses direction along a chain and moves `N` positions | 0 → 0 |

Use `sk` to leave a gap or move between attachment points. Use `bk` when you need to return to an earlier position while continuing in the same direction. The `r[N]` command is primarily used after a chain to work back along it: `r[2]` begins in the second chain from the hook, while `r[3]` begins in the third.

> [!NOTE]
> `r[N]` reverses direction within the current instruction sequence, whereas `turn` completes and turns the current round or row. They are not interchangeable.

See [Position controls](/docs/dsl/shaping#position-controls) and [Branching](/docs/dsl/shaping#branching) for examples.

### Color command

Use `col` or `color` before the stitches that should receive a color. Color commands do not consume or produce stitches.

| Command | What it does |
|---|---|
| `col[#RGB]` | Selects a color using a three-digit hexadecimal value |
| `col[#RRGGBB]` | Selects a color using a six-digit hexadecimal value |
| `col[N]` | Reuses the color at one-based index `N` in the project palette |
| `col[0]` | Clears the current selection and returns subsequent stitches to the default appearance |

`color[...]` is the full-length alias for `col[...]`. A color remains active for subsequent stitches in the same part until another color command changes it. The current selection resets when a part ends, but the palette is shared across the entire project. Each distinct hexadecimal color is added to that palette in the order it is first defined, so a palette index must be defined before it can be referenced.

The `#` inside a hexadecimal parameter is part of the color value and does not begin a comment. See [Working with colors](/docs/dsl/writing-instructions#working-with-colors) for palette and color-changing examples.

### Assembly commands

Assembly commands connect stitches that already exist. They create structural relationships between parts — or between two areas of one part — so the connected pieces can influence one another during simulation.

| Command | What it does |
|---|---|
| `join[Pn]` | Brings the last round of a previously defined part into the current working path |
| `SEW: A-B` | Connects [stitch selection](#selector-reference) `A` and [stitch selection](#selector-reference) `B` in their written order |
| `SEW: A~B`| Reverses [stitch selection](#selector-reference) `B`, then connects it to [stitch selection](#selector-reference) `A` |

Place `join[Pn]` within a round or row to bring in the last round of another part and continue working across both parts as a whole. The command neither copies the joined stitches nor creates new ones; subsequent instructions work into the stitches brought in from part `Pn`. See [Joining parts](/docs/dsl/multi-part#joining-parts) for details.

Write `SEW:` on its own line after both [selections](#selector-reference) have been worked. Sewing adds connections without changing either selection’s stitch count, and both sides must contain the same number of stitches. A hyphen pairs them in their selected order, while a tilde reverses the second selection before pairing.

A `SEW:` line must appear within the scope of one of the parts it connects. Multiple connections can be placed on one line by separating them with commas. See [Sewing parts](/docs/dsl/multi-part#sewing-parts) and [Sewing within a part](/docs/dsl/shaping#sewing-within-a-part) for complete examples.

Alternatively, you can use [selectors](#selector-reference) in `R0` to achieve joining. See [Begin with existing stitches](/docs/dsl/writing-instructions#begin-with-existing-stitches).

## Selector reference

Selectors identify stitches that have already been made. They make existing stitches accessible for use in a custom `R0` foundation or a `SEW:` command. Stitch numbering begins at `S1` within each round or row.

| Selector | What it selects |
|---|---|
| <span class="row-code">R3</span> | All stitches in `R3` of the current part |
| <span class="row-code">R3</span><span class="st-code">S6</span> | The sixth stitch in `R3` of the current part |
| <span class="row-code">R3</span><span class="st-code">S6:S8</span> | Stitches 6 through 8 in `R3` of the current part, inclusive, in *forward* order |
| <span class="row-code">R3</span><span class="st-code">S8:S6</span> | Stitches 6 through 8 in `R3` of the current part, inclusive, in *reverse* order |
| <span class="part-code">R3</span><span class="row-code">R3</span> | All stitches in `R3` of part `P1` |
| <span class="part-code">P1</span><span class="row-code">R3</span><span class="st-code">S6</span> | The sixth stitch in `R3` of part `P1` |
| <span class="part-code">P1</span><span class="row-code">R3</span><span class="st-code">S2:S5</span> | Stitches 2 through 5 in `R3` of part `P1`, inclusive, in *forward* order |
| <span class="part-code">P1</span><span class="row-code">R3</span><span class="st-code">S5:S2</span> | Stitches 2 through 5 in `R3` of part `P1`, inclusive, in *reverse* order |

Part code may be omitted only for the current part. Each selection must identify a round or row. A part code alone, such as `P1`, and a stitch code alone, such as `S6`, are not valid selectors. Any referenced part, round, or stitch position must already exist before the declaration of the selector.

See [Selecting stitches](/docs/dsl/writing-instructions#selecting-stitches) for complete guidance.

## Syntax limits

Knotly applies the following limits to keep instructions valid and models practical to simulate. Exceeding a limit causes an error when the pattern is parsed or run.

| Item | Limit or rule |
|---|---|
| Round range | At most 100 rounds or rows can be repeated using a range |
| Round stitch count | At most 1,000 stitches may be added to one round or row |
| Magic ring | At most 24 available spots can be specified or worked into a ring |
| Puff, bobble, popcorn | At most 8 components in one textured stitch |
| Compound stitch | At most 12 component instructions inside one compound increase or decrease |
| Turning chain | At most 5 leading `tch` stitches may be added in a row or joined round |

Knotly does not impose a fixed limit on the total number of parts or stitches in a project. You can write and run as many as your device can handle. However, keeping these numbers reasonably low is recommended for faster simulation and better performance.