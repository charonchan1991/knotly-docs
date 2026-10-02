# Shaping
Shaping is the process of controlling how a crocheted piece expands, contracts, bends, folds, and branches to form the intended structure. In Knotly, a piece’s shape is determined not only by its stitch counts, but also by where each stitch is placed and how it connects to the surrounding fabric.

Increases and decreases change the number of stitches between rounds or rows, loop-selection commands alter their attachment points, and position controls redirect the working path. These techniques can be used independently or combined to create anything from smooth curves and sharp corners to layered surfaces, openings, and complex branched forms.

## Increases and decreases
An increase produces multiple stitches from one root stitch, while a decrease combines multiple root stitches into one by working them together. Distributing these operations evenly creates gradual shaping; concentrating them in particular areas creates corners, curves, points, and asymmetrical forms.

Understanding [stitch counts](../quick-start.md#know-your-stitch-counts) is essential when working with increases and decreases. Make sure you are familiar with them before getting started.

### Increases
An increase works two or more stitches into the same stitch from the previous round. It consumes one root stitch but produces multiple final stitches, causing the fabric to expand.

Concentrated increases usually create sharper corners or waves, while evenly distributed increases produce smoother expansion.

The following table lists commonly used increase commands:

| Increase | XVA notation | U.S. terminology |
|---|---:|---:|
| Two-stitch single crochet increase | `V` / `XV` | `sc2inc` |
| Two-stitch half double crochet increase | `TV` | `hdc2inc` |
| Two-stitch double crochet increase | `FV` | `dc2inc` |
| Two-stitch treble crochet increase | `EV` | `tr2inc` |
| Three-stitch single crochet increase | `W` / `XW` | `sc3inc` |
| Three-stitch half double crochet increase | `TW` | `hdc3inc` |
| Three-stitch double crochet increase | `FW` | `dc3inc` |
| Three-stitch treble crochet increase | `EW` | `tr3inc` |
| Arbitrary increase (`N`: integer, `st`: stitch type) | `[N st]+` | `stNinc` |

If you are using U.S. terminology, use the syntax `stNinc` to construct an arbitrary increase, where `st` specifies the stitch type and `N` specifies the number of stitches to increase to. Possible stitch types in an arbitrary increase are: `sc`, `hdc`, `dc`, `tr`, and `dtr`. For example, `dc4inc` means working four double crochet stitches into one root stitch.

If you are using XVA notation, use the [compound method](#compound-increases-and-decreases) to construct an arbitrary increase. Place the stitch type — `X`, `T`, `F`, or `E` — and its quantity coefficient inside a pair of square brackets, then append an optional `+` if you want to make the increase explicit. The previous example can therefore be written as `[4F]` or `[4F]+` in XVA notation.

### Decreases

A decrease combines two or more consecutive root stitches into one. It consumes multiple stitches but produces only one, causing the fabric to narrow.

The following table lists commonly used decrease commands:
| Decrease | XVA notation | U.S. terminology |
|---|---:|---:|
| Single crochet two together | `A` / `XA`| `sc2tog` / `sc2dec` |
| Half double crochet two together | `TA` | `hdc2tog` / `hdc2dec` |
| Double crochet two together | `FA` | `dc2tog` / `dc2dec` |
| Treble crochet two together | `EA` | `tr2tog` / `tr2dec` |
| Single crochet three together | `M` / `XM` | `sc3tog` / `sc3dec` |
| Half double crochet three together | `TM` | `hdc3tog` / `hdc3dec` |
| Double crochet three together | `FM` | `dc3tog` / `dc3dec` |
| Treble crochet three together | `EM` | `tr3tog` / `tr3dec` |
| Arbitrary decrease (`N`: integer, `st`: stitch type) | `[N st]-` | `stNtog` / `stNdec` |

> [!TIP]
> In Knotly, `tog` and `dec` are interchangeable when using U.S. terminology.

If you are using U.S. terminology, use the syntax `stNtog` or `stNdec` to construct an arbitrary decrease, where `st` specifies the stitch type and `N` specifies the number of root stitches to combine into one. Possible stitch types in an arbitrary decrease are: `sc`, `hdc`, `dc`, `tr`, and `dtr`. For example, `dc4tog` means working four source stitches together as one double crochet decrease.

If you are using XVA notation, use the [compound method](#compound-increases-and-decreases) to construct an arbitrary decrease. Place the quantity and stitch type — `X`, `T`, `F`, or `E` — inside a pair of square brackets, then suffix with the mandatory `-` sign to identify the compound stitch as a decrease. The previous example can therefore be written as `[4F]-` in XVA notation.

### Compound increases & decreases
Standard increases and decreases use a single stitch type. A compound increase or decrease combines different stitch types into one shaping operation.

Compound increases are useful for creating fans, shells, corners, and textured clusters. To construct a compound increase, use square brackets to group the component stitches. You can append an optional `+` immediately after the closing bracket to make the increase explicit:
```
[sc, hdc, dc]+
```
This instruction works a single crochet, half double crochet, and double crochet into the same source stitch. It consumes one stitch and produces three.

The same compound increase can be written with an even more explicit command with an `inc` prefix:
```
inc[sc, hdc, dc]
```
Knotly supports compound decreases containing different stitch types, although they may not always be practical in real-world crochet. To create a compound decrease, add `-` after the brackets:
```
[sc, hdc, dc]-
```
This instruction works three differently typed root stitches together as one compound stitch. It consumes three stitches and produces one.

You can also use a more explicit variant with a `tog` or `dec` prefix:
```
tog[sc, hdc, dc]
```
```
dec[sc, hdc, dc]
```
Compound increases/decreases can be repeated by placing a quantity coefficient before the brackets:
```
4[X, T, F]+ // Repeat the compound increase four times
```
Each repetition consumes one root stitch and produces three new final stitches. The complete instruction therefore consumes four root stitches from the preceding round and produces twelve.


## Loop selection

Use **loop-selection commands** to specify which loop subsequent stitches should be worked into. These commands do not create stitches themselves, so their position within the instruction sequence matters.

By default, Knotly works through both loops of each stitch, except when working into chain stitches. For a chain stitch `ch`, the back loop (BLO) is preferred by Knotly unless another loop is specified. To change the default behavior, use a combination of the following **loop-selection commands**:

| Command | What it does |
|---|---|
| `flo` | works subsequent stitches through the **front loop only** |
| `blo` | works subsequent stitches through the **back loop only** |
| `both` / `bthl` | returns to working through **both loops** |
| `bump` | works into the **back bump** of a chain stitch |

Loop selection can affect both the structure and appearance of the final models in Knotly. Working into only the front or back loop changes where a stitch attaches to the preceding round or row. This can create a visible ridge, alter how the fabric bends or folds, and influence the model’s overall shape.

Knotly accounts for these attachment points in its physics-based simulation. In **Realistic mode**, the selected loop also changes how each stitch is positioned and rendered, producing a more accurate representation of the finished fabric.

### Front-loop & back-loop

A standard crochet stitch is usually worked through both loops at the top of the preceding stitch. This is also the Knotly's default behavior. Working through only one loop changes the stitch’s attachment point and leaves the other loop exposed.

Working into a single loop can also change how the fabric bends. A complete round of **front-loop only (FLO)** or **back-loop only (BLO)** can form a natural crease, allowing the following stitches to change direction more sharply. This is particularly useful when transitioning between a flat base and the vertical sides of a three-dimensional object.

Place any loop-selection command before the stitches it should affect:
```
R2: flo, 12X
```
You can change loop selection within the same round or row:
```
R2: flo, 6X, blo, 6X
```
You can also alternate loops by grouping the commands and stitches into a repeating sequence:
```
R2: 6(flo, X, blo, X)
```
A loop-selection command remains active until another loop-selection command appears or the current round or row ends. At the beginning of the next instruction line, Knotly returns to working through both loops automatically.

### Back bump

The `bump` command applies only when working into chain stitches:
```
R0: 9CH, turn
R1: bump, 9X, turn
```
The example above demonstrates how to work into the back bumps of a foundation chain. This leaves the two top loops undisturbed, producing a cleaner, more finished-looking edge.

## Position controls

Position controls move the current working position forward or backward without creating a new stitch.

### Skipping

Skipping a stitch in crochet means passing over a stitch from the previous round or row without working into it, usually by jumping straight to the next stitch or matching it with a chain space. Use `sk` or `K` to skip the next available stitch without creating a new one:
```
R0: 8ch, turn
R1: 3F, 2K, 3F, turn
```
The sequence in `R1` consumes eight stitches from the previous round but produces only six. Skipped stitches can create gaps, buttonholes, armholes, lace openings, and spaces beneath chain sections.

### Returning to an earlier position
The `bk` command moves the working position backward by one stitch without creating a new stitch or reversing the overall working direction. Prefix it with a quantity coefficient to move back several positions.

The `bk` command is useful when a branch must begin from an earlier position or when several structures need to share an attachment area. It only changes the working position and does not reverse the direction in which subsequent stitches are processed.

> [!WARNING]
> Because `bk` can return the working position to stitches that have already been passed, it interrupts the natural working flow and may produce unexpected connections. Avoid using it less necessary.

## Sewing within a part

You can reshape a part by using a `SEW:` line to connect two sets of stitches within it.

Although `SEW:` often connects separate parts, it can also link two sets of stitches within a single part. These extra connections do not create stitches or change the working sequence, but they can pull areas together to close an opening, join opposing edges, or form a fold.

For example, this piece is worked in **Joined rounds** mode. It widens, narrows, and is then sewn to its foundation to form a donut-shaped ring:

```
# Assuming current round mode is set to [Joined rounds]
R0: 20CH
R1: 20X
R2: 10(X, V)
R3: 30X
R4: 10(2X, V)
R5: 40X
R6: 10(3X, V)
R7-R11: 50X
R12: 10(3X, A)
R13: 40X
R14: 10(2X, A)
R15: 30X
R16: 10(X, A)
R17: 20X

SEW: R0-R17  // Sew the foundation round to the last round to form a donut ring
```
`SEW: R0-R17` pairs the 20 foundation chains with the 20 stitches in the final round, closing the remaining opening and drawing the two ends together. Both [selectors](./writing-instructions.md#selecting-stitches) omit a part code because they refer to the current part. Sewing adds no stitches, so the round counts remain unchanged; it only changes the shape by adding connections between stitches that were worked at different stages.

Place the `SEW:` line after both selections have been worked. The selections must contain the same number of stitches, and their pairing order should follow the intended seam. For the full syntax and examples that connect separate parts, see [Sewing parts](./multi-part.md#sewing-parts).

## Branching

Branches are secondary stitch paths that extend from a round or row before returning to the main working path. They can be used to construct petals, leaves, points, tentacles, fingers, lace sections, and other shapes that cannot be described as a single linear sequence.

### Creating a branch

A branch commonly begins with a chain worked from the current stitch. Because chain stitches do not consume stitches from the parent round, they extend away from the main working path.

Place the `r` command immediately after a chain to reverse the working direction and create a new branch. It must include a positive integer enclosed in square brackets using the format `r[N]`, where the value of `N` specifies how many positions to move in the reversed direction before processing the next instruction. Quantity coefficients are not allowed for the `r` command.

The `r` command almost always used in conjunction with a chain. When working back along a chain, `r[2]` is interpreted as beginning in the second chain from the hook, while `r[3]` begins in the third chain from the hook. A value of `N` greater than 3 is possible but uncommon in practice. This technique is primarily used to work back along a newly created chain, forming branches such as petals, leaves, fingers, and tentacles within an existing round or row.

For example, the following sequence creates a chain branch and then works back from it:
```
R1: 10CH, r[2], 9X
```
When the branch reaches the parent round from which it originated, Knotly automatically restores the original working direction and moves the current working position back onto the parent round. Instructions that follow can then continue along the parent round.

Unlike `turn`, the `r` command does not complete the current round or row. It changes direction within the same instruction sequence only.

It is also worth noting that using `r[N]` after a chain automatically generates *N - 1* [turning chain stitches](./writing-instructions.md#working-with-turning-chains). For example, `r[3]` produces two turning chain stitches. These stitches provide the height needed for the first stitch worked back into the chain.

> [!NOTE]
> Use `r[N]` to reverse direction within a branch. The `turn` command completes and turns the current round or row. These two commands serve different purposes and are not interchangeable.

> [!TIP]
> Use **Sketch mode** when working with `sk`, `bk`, or `r`. Its working-direction arrows make complex stitch placement easier to inspect.

### Anchoring and repeating branches

A slip stitch (`sl` or `ss`) is usually used to anchor a branch before continuing along the parent round. It is often used in conjunction with a skip command (`sk` or `K`) that helps with moving the working position between branches:
```
// ... Parent round omitted
R1: 10CH, r[2], 9X, K, SL  // Slip stitch back to the parent round when the branch ends
```
To repeat a branch sequence:
```
R0: 12CH
R1: 6(10CH, r[2], 9X, K, SL)
```
Each repeated group creates a chain branch, works back along it, moves to the next attachment point, and anchors the branch with a slip stitch. Keep the complete instructions for one branch inside parentheses when repeating it. This makes the relationship between the chain, reversal, return stitches, and attachment command easier to understand.

In the example above, repeating the group six times produces a six-pointed star composed of six similar branches, which can serve as the center of a snowflake.
