# Writing Instructions

Once you’re familiar with the [fundamentals](./fundamentals.md), you’re ready to write a pattern. This guide covers the essentials of writing patterns in Knotly: starting a part, repeating instructions, working with turning chains and colors, and selecting existing stitches.

## Starting a part

Every part begins with a foundation. In Knotly, the foundation is represented by `R0` while regular stitching begins at `R1`. Knotly can infer `R0` in some situations, but defining it explicitly makes the construction clearer and gives you greater control over how the part begins.

### Magic rings

A magic ring (or magic circle) is an adjustable starting loop used for crochet projects worked in the round. It can be pulled tightly closed to prevent a hole from forming in the center, making it ideal for circular or three-dimensional pieces such as amigurumi, hats, and round motifs.

The Knotly command for a magic ring is `mr`. It can include an optional numeric parameter enclosed in square brackets, such as `mr[6]`, which specifies the exact number of virtual spots available in the ring. Define the magic ring in `R0`, then work the first round of stitches into it:
```
# Assuming current round mode is set to [Joined rounds]
R0: MR
R1: 6X
```
When the project uses **Joined rounds** mode, Knotly can usually infer the magic ring from the instructions in `R1`. The example above can therefore be shortened to:
```
# Magic ring is assumed when R0 is missing in [Joined rounds] mode
R1: 6X
```
Defining `R0` explicitly is still recommended when you want the foundation to be immediately clear to anyone reading the pattern.

> [!TIP]
> Using less than 10 stitches in a magic ring is recommended as the ring will not close tightly when there are too many stitches. If you need to begin with more stitches, consider using a foundation chain ring instead.

### Foundation chains

A foundation chain is a series of chain stitches made at the beginning of a crochet project to provide a base for the first row. Use a foundation chain to begin flat pieces or shapes worked around both sides of a chain.

In Knotly, a foundation chain always consists of a series of `ch` stitches followed by an end-of-round `turn` command in `R0`. To create a flat piece, add `turn` after the foundation chain so that the first row is worked back along it:
```
R0: 9CH, turn  // Foundation chain
R1: 9X, turn  // First row
```
When the project uses **Rows** mode, Knotly will infer the foundation chain of equal length from `R1`. The example above can therefore be shortened to:
```
# A foundation chain is assumed when R0 is missing in [Rows] mode
R1: 9X  // 'turn' can be omitted on [Rows] mode
```
Defining the foundation chain explicitly in `R0` gives you direct control over its length and construction, so it is generally a good practice.

### Foundation chain rings
A foundation chain ring (or foundation chain loop) is a closed loop of chain stitches. Unlike a magic ring, it leaves a fixed opening in the center, making it useful for motifs, coasters, granny squares, decorative openings, and other tubular or circular constructions.
```
# Assuming current round mode is set to [Joined rounds]
R0: 12CH  // This line CANNOT be omitted
R1: 6(X, V)
```
`R0` cannot be omitted in this case. When no foundation is provided in **Joined rounds** mode, Knotly assumes that the part begins with a magic ring rather than a chain ring.

### Begin with ovals

A foundation oval in crochet is an elongated, rounded starting ring or base created by working around both sides of a foundation chain. It is commonly used in amigurumi with a wide base, bags & baskets, footwear, and in some garments as well.

To create an oval, begin with a foundation chain and turn the working direction before crocheting around both sides of it:
```
# Assuming current round mode is set to [Joined rounds]
R0: 9CH, turn  // Foundation chain
R1: 8X, W, 7X, V  // '$sl' can be omitted on [Joined rounds] mode
```
In this example, the stitches in `R1` are distributed around both sides and ends of the foundation chain. Because the project is set to use **Joined rounds** mode, Knotly closes the completed `R1` automatically without needing an [end-of-round command](./fundamentals.md#round-modes-and-end-of-round-controls).

> [!WARNING]
> Don't use `r[N]` command to create the foundation if you need an oval.

### Begin with existing stitches

A new part can use stitches from another part as its foundation. Place one or more [stitch selectors](./writing-instructions.md#selecting-stitches) in `R0` to identify the existing stitches into which the new part will be worked.

For example, the following two-layer skirt begins in the stitches of `R10` from the body:
```
P1: Body
// ... Earlier rounds omitted
R10: 36X

P2: Outer skirt
R0: P1R10  // Select all stitches from P1R10
R11: FLO, 36(FW)  // Work into the front loops of the selected stitches

P3: Inner lining
R0: P1R10  // Select all stitches from P1R10
R11: BLO, 36(F)  // Work into the back loops of the selected stitches
```
By convention, when a part continues from a parent part, its first stitching instruction uses the round number following the selected round of the parent part. However, starting the new part with the traditional `R1` round code is also perfectly acceptable.

You can combine one of the layers — either `P2` or `P3` — with the main body in `P1` to reduce the number of parts used. However, defining each layer as a separate part often makes the project’s construction clearer. A combined version of the above pattern looks like this:
```
P1: Body
// ... Earlier rounds omitted
R10: 36X
R11: BLO, 36(F)  // The inner lining is now worked as part of P1

P2: Outer skirt
R0: P1R10  // Select all stitches from P1R10
R11: FLO, 36(FW)  // Work into the front loops of the selected stitches
```
A selection in `R0` does not create another copy of the selected stitches. Instead, it tells Knotly to use the selected stitches as the structural foundation of the new part. You can select an entire round, a single stitch, or a range of stitches as foundation. For complete guidance on using selectors, see [Selecting stitches](./writing-instructions.md#selecting-stitches).

A part can also start a part from multiple selections. This is useful when connecting two existing pieces with a newly crocheted section. For example, you can use this technique to join two legs while beginning a doll’s body:

```
P1: Left leg
// ... Earlier rounds omitted
R6: 12X

P2: Right leg
// ... Earlier rounds omitted
R6: 12X

P3: Body
R0: P1R6, P2R6  // Select the final rounds of both legs
R7: 24X  // Join the selections and work them as one round
```
When a part begins from existing stitches, Knotly treats it as structurally connected to the referenced part or parts. The connected pieces are therefore simulated together as a single assembly, allowing their shapes to influence one another. Parts that are not connected through a shared foundation, joining, or sewing are simulated independently.

> [!TIP]
> Alternatively, you can use a `join` command to connect two parts and achieve a similar result. See [Joining parts](./multi-part.md#joining-parts) for details.

## Repeating an instruction
After establishing a foundation, describe each round or row as an ordered sequence of stitches and commands. Knotly processes instructions from left to right while tracking the current working position, loop selection, and stitch count.

Use repetition to keep your pattern instructions clean, concise, and readable.

### Repeating a stitch

A [stitch command](./language-reference.md#stitch-reference) without a quantity coefficient is worked once only. To repeat it, place a positive integer — called a **coefficient** — immediately before the stitch command with an optional space in between. The coefficient specifies how many times the stitch should be worked:

```
R1: 6X
```
This instruction works six single crochet stitches into the preceding round. It is equivalent to writing:
```
R1: X, X, X, X, X, X  // Equivalent to '6X' or '6sc'
```
Use **commas** to combine different stitches and commands into a sequence:
```
R2: 3X, V, 2X
```
> [!TIP]
> Knotly can automatically combine consecutive stitches and commands using coefficients. Enable **Merge consecutive stitches** in the editor panel’s formatter.

### Repeating a sequence

Enclose a comma-separated sequence in parentheses and put a quantity coefficient before it to repeat the whole group. For example:
```
R1: 6X
R2: 6V
R3: 6(X, V)
```
In `R3`, each group of `(sc, sc2inc)` — or `(X, V)` as in the XVA notation — consumes two root stitches from `R2` and produces three. Repeating the group six times consumes all 12 stitches from `R2` and produces a final of 18. This is equivalent to writing `sc, sc2inc` or `X, V` six times.

A group without a coefficient is worked once, so you can use parentheses to separate meaningful sections of an instruction. Take the [oval example](#begin-with-ovals) above as an example: the groups distinguish the first side, one end, and the return side with the other end:
```
# Assuming the current round mode is set to [Joined rounds]
R0: 9CH, turn  // Foundation chain
R1: (8X), (W), (7X, V)  // This is the same as the original oval example
```
The parentheses do not change the stitch sequence or count. They simply make the oval's construction easier to read.

Groups can be nested when a longer sequence contains a smaller repeated unit:
```
R3: 2(3(X, V), X)
```
This instruction line will first expand to:
```
R3: 3(X, V), X, 3(X, V), X
```
And finally:
```
R3: (X, V, X, V, X, V), X, (X, V, X, V, X, V), X
```
All these three instructions are valid and equivalent.

Behind the scenes, Knotly expands the inner group for each repetition of the outer group. Keep the commas inside the parentheses so the commands remain part of the group.

> [!WARNING]
> Do not confuse parentheses with square brackets. Parentheses group instructions for repetition, while square brackets specify parameters or create [compound increases and decreases](./shaping.md#compound-increases-and-decreases).

### Repeating rounds or rows

To use the same instructions for several consecutive rounds or rows, write a range of round codes followed by one instruction sequence:
```
R1: 6X
R2: 6V
R3-R5: 12X  // This line will create and apply to R3, R4, and R5
```
In the example above, Knotly treats `R3-R5` as three separate rounds, each containing 12 single crochet stitches. The range includes both endpoints, and its end number must be greater than its start number.

> [!TIP]
> The counter gutter on the right side of the editor shows the number of repetitions as a multiplier.

Knotly does not automatically adjust the repeated instrunctions to account for increases or decreases. For example, `6(sc, sc2inc)` or `6(X, V)` consumes 12 root stitches and produces 18. Repeating it unchanged in the next round would leave six of those 18 stitches unworked. Conversely, `6(sc, sc2tog)` or `6(X, A)` consumes 18 root stitches and produces 12. While the editor may not report an alert, repeating it will cause a runtime error because only 12 root stitches are available for the second iteration. Write a separate instruction line whenever the stitch count needs to change.

## Working with turning chains

Turning chains raise the working yarn to the height of the first stitch in a new row or joined round. Place `tch` or `$ch` **at the beginning** of the instruction line when you want to specify them explicitly. Unlike an ordinary chain, Knotly treats turning chains as height aids only. This means that they are not meant to be worked into, do not count toward the round or row’s stitch total, and therefore cannot be targeted by a [stitch selector](#selecting-stitches).

> [!WARNING]
> Don't use `tch` for chains that are meant to form part of the fabric or a branch. Use ordinary `ch` instead.

Generally speaking, you do not need to specify turning chains in **Joined rounds** mode. In fact, they are discouraged in this mode because they can affect the simulation and make the preview less preferable.

> [!NOTE]
> Turning chains are not available in **Continuous rounds** mode because those rounds have no turned or joined starting edge.

In **Rows** mode, however, turning chains are encouraged. In fact, Knotly would add the needed turning chains automatically after a turn, based on the height of the first stitch, to achieve the best preview. For example, this flat double-crochet swatch needs no written `tch` commands:
```
R0: 6CH, turn
R1-R3: 6F, turn  // Two turning chains will be generated automatically at the beginning
```
If you want make the turning chains explicit, the above example can also be written as:
```
R0: 6CH, turn
R1: 2TCH, 6F, turn  // Make the leading turning chains explicit if you want
```
Knotly allows at most five turning chains at the beginning of a round or row. If you choose to specify them, provide enough height for the first stitch. Knotly will report an error otherwise.

> [!NOTE]
> The reversal command `r[N]` will also mark the first *N - 1* chains of a branch as turning chains when you work back along it. See [Creating a branch](./shaping.md#creating-a-branch) for details.


## Working with colors

Use the color command `color` — or `col` for short — before the stitches that should receive a color. Color commands do not consume or produce stitches. Enclose a three- or six-digit hexadecimal color value in square brackets as the command's parameter:
```
R1: color[#8BC46C], 6X
R2: 6V  // This line also receives the same color as R1
```
The color applies from the command onward. In this example, `R2` remains green without another color command. Color changes carry forward through later instructions in the **same part** until another color command changes them:

```
R1: col[#8BC46C], 6X
R2: col[#F5C647], 6V  // Stitches on this line now receive a different color
```

Knotly clears the current color when a part ends. A new part thus will require its own color command if it needs to use the color from the preceding part. Use `color[0]` or `col[0]` to clear the current color selection and returns subsequent stitches to the default appearance.

> [!TIP]
> The hexadecimal `#` inside the parameter of a color command is part of the color value, not the start of a comment.

> [!TIP]
> You can click on the color swatch inside a color command to choose a color intuitively from a color picker.

### Reusing an existing color

Knotly automatically tracks each project’s color palette internally. You can reuse a previous color by referencing its index in the palette. Changing a color where it is defined updates every reference to it in the project. 

Each distinct hexadecimal color is added to the project's palette in the order it first appears. A positive integer as the parameter reuses a color already defined in that palette: `col[1]` selects the first color, `col[2]` the second, and so on. Always define a color before referencing its index. Referencing an undefined palette index produces an error at run time. 

```
R1: col[#8BC46C], 6X
R2: col[#F5C647], 6V
R3: col[1], 12X  // Reusing the first color
R4: col[3], 12X  // Referencing an undefined color produces an error
```
You can define your entire palette in `R0`, then refer to the colors by their palette indices throughout the pattern. This keeps the instructions cleaner and makes colors easier to maintain.

```
// Defining the palette for the entire project
R0: color[#8BC46C], color[#45973C], color[#F5C647]

// Using color indices to refer to a color in the palette
R1: col[1], 18CH  
R2: col[2], 18X
R3: col[3], 18X
R4: col[1], 18X
R5: col[2], 18X
R6: col[3], 18X
```
Each project has **one and only one** palette shared by all its parts. Colors introduced in later parts will be appended to the same palette. Once a color is defined, its palette index remains the same across all parts of the project. Re-defining a same color will not affect its index in the palette.
```
P1
R0: color[#F5C647], color[#8BC46C]  // Defining colors for P1
// ... P1 stitching omitted

P2
R0: color[#45973C]  // This color is appended to the same palette as P1's
R1: col[1], 18CH  // Referencing P1's color
R2: col[2], 18X   // Referencing P1's color
R3: col[3], 18X   // Referencing P2's color
```
### Alternating colors in a round

You can alternate colors stitch by stitch within a single round or row:
```
R1: color[#8BC46C], 6X
R2: color[#F5C647], 6V
R3: 6 (color[1], X, color[2], X)
R4: 6 (color[2], X, color[1], X)
```
Here, `color[1]` selects the green introduced in `R1`, and `color[2]` selects the yellow introduced in `R2`. Each repetition in `R3` produces a green stitch followed by a yellow one; `R4` reverses the order to create a checkerboard-like pattern. After `R4`, green — the last selected color — remains in effect until another color command changes it.


## Selecting stitches

**Selectors** identify stitches that already exist in the pattern. A selector consists of a round code, optionally preceded by a part code and followed by a stitch code. Stitch codes start at `S1` for each round or row, which identifies the first stitch in the selected round or row:

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

Selectors must always point to parts, rounds, and stitch positions that have already been defined. You can omit the part code only when selecting stitches from the current part. A part code alone, such as `P1`, is not a valid stitch selector.

Use a colon between two stitch codes to select a range of stitches in a round or row. The order in a stitch range matters: `S2:S5` and `S5:S2` contain the same four stitches but present them in opposite directions. A stitch code alone, such as `S1`, or a stitch range without a round code, such as `S1:S3`, is also invalid because it does not identify which round or row contains those stitches. Leading [turning chains](#working-with-turning-chains) do not receive stitch codes and thus cannot be selected.

Selectors are used both in a foundation and as part of the instruction for a `SEW:` line. They only serve as the bases to be worked into and do not duplicate the selected stitches.

### Using selectors in foundation

When several selectors appear in a foundation, Knotly combines their results in the written order:
```
P1: First strip
R0: 6CH, turn
R1: 6X, turn

P2: Second strip
R0: 6CH, turn
R1: 6X, turn

P3: Joining section
R0: P1R1S6:S1, P2R1S6:S1  // Reversing selection order to maintain alternating row direction
R2-R4: 12X, turn  // Working on top of P1 and P2 as a whole
```
Here, Knotly selects the six stitches from `P1` in reverse order, followed by the six stitches from `P2` in reverse order. The resulting 12-stitch foundation allows `P3` to continue across both strips as a single piece. The selectors in `R0` establish a [foundation from existing stitches](#begin-with-existing-stitches). 

### Using selectors in SEW commands

Outside `R0`, use selectors within an assembly instruction such as `SEW:` rather than as standalone stitch commands. See [Sewing parts](./multi-part.md#sewing-parts) for complete guidance.
```
P1: First strip
R0: 12ch, turn
R1-R2: 12sc, turn

P2: Second strip
R0: 12ch, turn
R1-R2: 12sc, turn

SEW: P1R2-P2R2S12:S1
```
In this example, <code><span class="part-code">P1</span><span class="row-code">R2</span></code> selects all 12 stitches in the last row of the first strip. <code><span class="part-code">P2</span><span class="row-code">R2</span><span class="st-code">S12:S1</span></code> selects the 12 stitches in the last row of the second strip in reverse order. The `-` sign pairs the two selections in their written order: `P1R2S1` connects to `P2R2S12`, `P1R2S2` connects to `P2R2S11`, and so on.

Both strips retain their original stitches, but Knotly treats them as a connected assembly during simulation.
