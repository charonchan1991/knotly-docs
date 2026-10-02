# Multi-part Objects

Many crochet projects are made from pieces that are worked separately and assembled later. In Knotly, each piece is a **part** with its own foundation, rounds or rows, and part code. Parts can remain independent, or they can be connected by working from existing stitches, joining during a round, or sewing selected stitches together. Connected parts are simulated as one assembly, so their shapes can influence one another.

## Choosing how to work

Give each separately constructed piece a unique part code and, optionally, a descriptive title, such as `P1: Body` or `P2: Ear`. Always define a part before referring to it from another part. Referencing stitches that do not exist will result in a runtime error. See [Parts](./fundamentals.md#parts) for the basic pattern structure.

Decide which pieces need a structural connection. You can always position independent parts manually in the scene, but do keep in mind that they are simulated separately. If one piece must continue from stitches in another, select those stitches in the new part as `R0`; see [Begin with existing stitches](./writing-instructions.md#begin-with-existing-stitches) for details. Use a [join](#joining-parts) when the working path should incorporate another part’s last round, or [sewing](#sewing-parts) when two or more independent parts should be attached to each other.

Knotly keeps one color palette for the whole project. A later part can [reuse a color](./writing-instructions.md#reusing-an-existing-color) with an index such as `col[1]`, but the active color itself resets when a part ends, so select it again in each new part if you want to keep using that color. [Stitch selectors](./writing-instructions.md#selecting-stitches) are used to identify existing stitches across parts. Keep these codes stable once another instruction refers to them.

## Joining parts

Place `join[Pn]` within the current round or row, where the parameter `Pn` is the code of any previously defined part. The command brings that part’s **last round or row** into the current working position. It does not copy the stitches or create new ones. Subsequent instructions work into the stitches brought in from the joined part.

The following example joins two 12-stitch pieces to form a structure that could serve as the legs of an amigurumi doll:

```
# Assuming the current round mode is set to [Joined rounds]
P1: Left leg
R1: col[#FDC3CE], 6sc
R2: 6sc2inc
R3: 12sc

P2: Right leg + Body
R1: col[1], 6sc
R2: 6sc2inc
R3: 12sc
R4: 12sc, join[P1], 12sc  // Bringing in the last round of P1 after the first 12 stitches
R5: 24sc
```

In `P2`'s `R4`, the first 12 single crochet stitches work across `P2`’s previous round. The command <code><i>join</i>[<span class="part-code">P1</span>]</code> then makes the 12 stitches of `P1`’s last round available, and the following 12 single crochet stitches work into them. `R4` therefore produces 24 final stitches, which `R5` can work on as one round. The two lobes become a connected assembly rather than two independently simulated objects.

> [!WARNING]
> The target part must already be defined and cannot be joined to itself or joined a second time. Knotly does not allow `join` in **Continuous rounds** mode.

In some cases, you can achieve the same result as `join` by using selectors in `R0`, though this requires a third part. The above example can be rewritten as follows:
```
# Assuming the current round mode is set to [Joined rounds]
P1: Left leg
R1: col[#FDC3CE], 6sc
R2: 6sc2inc
R3: 12sc

P2: Right leg
R1: col[1], 6sc
R2: 6sc2inc
R3: 12sc

P3: Body
R0: col[1], P1R3, P2R3
R4-R5: 24sc
```
The `join` approach often follows the natural crocheting process more closely, while using selectors in `R0` makes the project’s structure more explicit and the pattern easier to follow. Choose the approach you’re most comfortable with or the one that best suits your design. Check out [Begin with existing stitches](./writing-instructions.md#begin-with-existing-stitches) if you prefer the latter.

## Sewing parts

Use a `SEW:` line to connect stitches that have already been made. Sewing adds connections between existing stitches without creating new ones, so it does not change either part’s stitch count.

A `SEW:` line uses [stitch selectors](./writing-instructions.md#selecting-stitches) to identify two sets of stitches to connect. Separate the selectors with a hyphen (`-`) to pair stitches in their written order, or a tilde (`~`) to reverse the second selection before pairing. For sewing to succeed, both selections must contain the same number of stitches.

Note that a `SEW:` line must appear within the scope of one of the parts it connects. Because selectors can only reference stitches already defined, place the line after both sets of stitches have been worked — usually at the end of the second part’s instructions. Placing it outside the scope of both parts produces an error and thus should be avoided.

This example sews together the last rows of two flat strips:

```
P1: First strip
R0: 12ch, turn
R1-R2: 12sc, turn

P2: Second strip
R0: 12ch, turn
R1-R2: 12sc, turn

SEW: P1R2-P2R2S12:S1  // Selecting P2's last round in reverse order
```
You can also write it with a tilde:
```
P1: First strip
// ...

P2: Second strip
// ...

SEW: P1R2~P2R2  // Using a tilde to reverse second selection before pairing
```
`P1R2` selects all 12 stitches in the first strip’s last row, while `P2R2S12:S1` — or connected by a tilde as in `P1R2~P2R2` — selects the 12 stitches in the second strip’s last row in reverse order. Knotly pairs the stitches in the order selected. Reversing one side is often necessary when the edges face opposite directions. An incorrect order can twist or cross the seam especially, when working in rounds.

You can also use several `SEW:` lines to attach different areas. For example, replace the full-width seam above with two short seams to connect only the ends and leave the middle unsewn:

```
P1: First strip
R0: 12ch, turn
R1-R2: 12sc, turn

P2: Second strip
R0: 12ch, turn
R1-R2: 12sc, turn

SEW: P1R2S1:S3-P2R2S12:S10  // Or using a tilde -> P1R2S1:S3~P2R2S10:S12
SEW: P1R2S10:S12-P2R2S3:S1  // Or using a tilde -> P1R2S10:S12~P2R2S1:S3
```

Each line connects three pairs of stitches. Check both the number of stitches and the direction of each selection before running the pattern.

You can place multiple sewing connections on one `SEW:` line by separating them with commas. The preceding example can be written as:
```
P1: First strip
// ...

P2: Second strip
// ...

// Two SEW lines are combined into one with a comma
SEW: P1R2S1:S3-P2R2S12:S10, P1R2S10:S12-P2R2S3:S1
```
While this makes the pattern more compact, separate lines are usually easier to read, especially when there are ranges inside the selectors.

> [!NOTE]
> Sewing within a part is also possible. To shape a single part by sewing two areas of it together, see [Sewing within a part](./shaping.md#sewing-within-a-part).

## Naming a multi-part object

Knotly groups structurally connected parts into one simulated object. To name that object, add a heading with a **compound code** listing all its member part codes, separated by `+`:

```
// Place the title line before the member parts
P1+P2: Some Doll

// Part definitions begin
P1: Left leg
// ...
P2: Right leg + Body
// ...
```

The heading can also appear after the part definitions:

```
P3: Part A
// ...
P4: Part B
// ...
P5: Part C
// ...

// Alternatively, you can place the title line after the member parts
P3+P4+P5: Another multi-part object
```
A compound heading names an assembly; it does not connect the parts or contain stitching instructions. Knotly determines membership from actual stitch connections — such as a shared foundation and a `join` or `SEW:` command.

For the heading’s name to apply, it must list exactly the parts in the connected assembly. Without a heading, the parts are still grouped and simulated together, and Knotly generates a temporary name for the assembly from the member parts' individual names.
