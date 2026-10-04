# Fundamentals

To help Knotly bring your ideas to life, you will need to learn the crochet language that Knotly speaks. Knotly uses a case-insenitive domain-specific language (DSL) whose commands are largely based on crochet terminology widely recognized by crocheters around the world. If you already have experience with text-based crochet instructions, you are almost ready to go.

Don’t worry if you don’t — this guide will walk you through everything you need to know, step by step.


## Anatomy of a pattern

A Knotly pattern is organized into parts, rounds or rows, and comma-separated instructions. Understanding this structure makes patterns easier to write, navigate, and troubleshoot.

### Parts

A project can contain one or more independently constructed parts. When a project contains multiple parts, keep each part’s instructions directly beneath its heading to keep them clearly separated and organized.

A typical multi-part Knotly project looks something like this:

```
// Instructions for P0 go here, if any

P1: Body
// Instructions for P1 go here

P2: Head
// Instructions for P2 go here
```

Each part begins with a unique identifier known as a **part code**, optionally followed by a descriptive title separated from the code by a colon.

Part codes always begin with the letter `P`, followed by a number. For example, to define a part that will serve as the body of an amigurumi doll, write `P1: Body`. Each part code must be unique within a project because Knotly uses it to associate each set of instructions with its corresponding object in the scene. Part codes do not have to begin with `P1` or follow the natural numbering sequence, but numbering them in the order in which they are worked is a good practice.

Knotly will assign any instructions before the first part heading to the default part, `P0`. If you are creating a single-part project, you can omit the part heading entirely because the default part code `P0` will be assigned to your pattern automatically.

Part codes will appear in the selection dropdown in the editor panel as well as beneath the selected objects in the 3D scene, making it easier to navigate through your project.

> [!WARNING]
> Changing an existing part’s code can cause a duplicate part-code error or create inconsistent references throughout the project. It also resets any saved position and rotation data associated with that part. Proceed with caution if you must make this change.

Although part titles are optional, they do make complex projects easier to navigate and understand. Just like part codes, titles also appear in the selection dropdown in the editor panel as well as beneath the selected objects in the 3D scene.

### Rounds and rows

Each round or row begins with an identifier known as a **round code**, followed by a colon and a sequence of instructions. Within a part’s instruction scope, each non-empty line represents a new round or row unless it begins with a different type of identifier.

Round codes always start with the letter `R` and are numbered sequentially:

```
R1: 6sc
R2: 6sc2inc
R3: 6(sc, sc2inc)
```

Knotly uses the same `R` prefix for both rounds and rows. Whether an instruction is interpreted as a joined round, part of a continuous spiral, or a flat row depends on the project’s default round mode. You can override the default round mode and explicitly tell Knotly how to interpret the current line by using [end-of-round commands](./fundamentals.md#round-modes-and-end-of-round-controls) at the end of the line.

Keep rounds and rows in their intended working order and group them beneath the appropriate part:

```
P1: Body
R1: 6sc
R2: 6sc2inc
// ...

P2: Tail
R1: 4sc
R2: 4sc
// ...
```

The round code is optional in an instruction line but it is highly recommended. If they are omitted, Knotly treats each non-empty instruction line as the next round or row in the sequence and automatically generates a round number behind the scenes. Explicit round codes improve readability and make individual stitches easier to reference later.

> [!WARNING]
> Changing the round code on an existing line may create duplicate round codes and/or inconsistent references throughout the project, especially if the part is connected to other parts either by sewing or by joining. Proceed with caution when making this change.

Although not recommended, round codes can be duplicated or skipped within a part’s scope. When a round code is duplicated, every line is still executed, but only the first occurrence can be referenced elsewhere. Skipping a round number disrupts the natural numbering sequence and may cause reference issues. Avoid doing so unless you are intentionally continuing the numbering of a parent part when [starting from existing stitches](./writing-instructions.md#begin-with-existing-stitches).

> [!TIP]
> You can have Knotly automatically manage all round codes by enabling **Normalize round codes** in the editor panel’s formatter.


### R0 foundation

`R0` always represents the foundation of a part. It establishes the structure into which the first regular round or row is worked. If `R0` is omitted, Knotly infers it from the current round mode and the instructions provided in `R1`, the first instruction line of the part. Regular stitching generally begins at `R1`. Although Knotly can infer the foundation in some situations, defining `R0` explicitly makes the pattern’s construction easier to understand and gives you greater control over how the part begins.

For example, a circular piece can begin with a magic ring:

```
R0: mr  // This line can be omitted when round mode is set to [Joined rounds]
R1: 6sc
```

A flat piece can instead begin with a foundation chain:
```
R0: 9ch, turn  // This line can be omitted when round mode is set to [Rows]
R1: 9sc, turn
```

To begin with a foundation chain ring, you will need to make `R0` explicit to override the default:
```
# Assuming current round mode is set to [Joined rounds]
R0: 7ch  // This line CANNOT be omitted because a magic ring is assumed when missing
```
For more information about default foundation behavior, see [Starting a part](./writing-instructions.md#starting-a-part).


### Stitches and commands

Separate stitches and commands within a round or a row using **commas** in an instruction line. Knotly processes them from left to right:
```
R1: 3sc, sc2inc, 3sc
```
Stitches and commands can be nested inside parentheses. Commas inside parentheses or square brackets remain part of the enclosed instruction and do not divide the outer sequence:
```
R2: 2(sc, sc2inc), [sc, hdc, sc]+, 3sc
```
In the example above, parentheses create a repeatable group, while square brackets create a compound increase with different stitch types. An inner sequence of stitches and commands has higher priority and is processed before the outer sequence. For more information about how to use parentheses, see [Repeating a sequence](./writing-instructions.md#repeating-a-sequence). For information about how to construct a compound stitch, see [Compound increases and decreases](./shaping.md#compound-increases-and-decreases).

See [Language Reference](./language-reference.md) for a complete list of all supported stitches and commands that you can use in an instruction line.

### Comments

You can add comments using either `#` or `//`. Knotly ignores everything following the comment marker until the end of the line:

```
# Begin with a magic ring
R1: 6sc  // Work six single crochets into the magic ring
R2: 6sc2inc  // Increase to twelve by working two stitches into each one from the previous round
```

Comments can occupy an entire line or follow an instruction. They are useful for recording notes, reminders, and explanations without affecting the simulation.

> [!NOTE]
> A hexadecimal color value such as `col[#000]` is not treated as a comment because the `#` appears within the color command’s square-bracketed parameters and is therefore part of the command.

## Round modes & end-of-round controls

A project’s **round mode** determines what Knotly does when it reaches the end of each round or row when no explicit end-of-round command is present. It specifies whether the last stitch is joined to the beginning to form a closed round, the work continues directly into the next round to form a spiral, or the piece is turned so that the next row is worked in the opposite direction, back and forth.

The selected default mode applies throughout the project. You can override it for a particular line by placing **end-of-round commands** such as `$sl`, `-$sl`, or `turn` at the end of that line. Keeping this in mind is especially helpful when combining multiple round modes within the same project.

### Joined rounds

In **Joined rounds** mode, Knotly closes each round by connecting its end to its beginning with a round-closing slip stitch. The next round then begins from the closing point of the previous round. This is the default round mode in Knotly.

The end-of-round command for this mode is `$sl` or `$ss`. When this is the project’s default mode, Knotly creates the closing connection automatically and no end-of-round command is required.

In this mode, you do not need to add an end-of-round command to every line because Knotly closes each round automatically. Add the command only when you want to make the closure explicit or override a different default mode for a particular round.

To close a particular round when another mode is active:

```
R3: 18sc, $sl  // This round will be closed regardless of the current round mode
```

The `$sl` / `$ss` command tells Knotly to join the end of the current round to its beginning with a virtual slip stitch. It must appear at the end of the round.

> [!NOTE]
> The `$sl` / `$ss` is a round-closing command that mimics a closing slip stitch in real life, whereas `sl` / `ss` adds an ordinary slip stitch to the instruction sequence. These commands are not interchangeable.

Because the end and beginning of each round are connected, joined rounds create distinct circular layers. This mode is useful for amigurumi dolls, some motifs, granny squares, and other pieces in which every round is completed before the next one begins.

During the design process of a closed-round project, you may want to try different stitch combinations in various positions before completing a round. Enable **Keep last round open until finished** to prevent the current round from closing automatically until all available positions in the previous round have been used. This feature is available only in **Joined rounds** mode.

### Continuous rounds

In **Continuous rounds** mode, the end of one round flows directly into the beginning of the next without a closing slip stitch. This creates an uninterrupted spiral rather than a series of individually joined circles. Although there is no physical join between rounds, each instruction line still defines a logical round. Round codes therefore remain important for counting stitches, referencing specific rounds, and keeping the pattern readable.

> [!WARNING]
> Working in continuous rounds is currently an experimental feature. The resulting shape may appear distorted in some patterns, so use this mode with caution.

The end-of-round command for this mode is `-$sl` or `-$ss`, literally meaning *no closing slip stitch*. It must appear at the end of the round. No end-of-round command is required when this is the project’s default mode. 

To leave a particular round open when another mode is selected:

```
R3: 18sc, -$sl  // This round remains open regardless of the current round mode
```

The minus sign indicates that the closing slip stitch should be omitted. If several consecutive rounds need to remain open, selecting **Continuous rounds** as the project’s default mode is more concise than adding `-$sl` or `-$ss` to every line.

> [!TIP]
> Keep each spiral round on a separate line even though the stitches form one continuous path. Clear round boundaries make increases, decreases, stitch counts, and references much easier to follow.

### Rows

In **Rows** mode, each completed row is turned so that the following row is worked back across the preceding one in the opposite direction.

The end-of-round command for this mode is `turn`. By default, it leaves the current round open unless an explicit `$sl` / `$ss` command is present in the same instruction line.

When **Rows** is the project’s default mode, Knotly turns the work automatically at the end of every row. You do not need to add `turn` to each line.

To turn after a particular line when another mode is selected, place the `turn` command at the end:

```
R1-R5: 9sc, turn  // These rows will be worked back and forth
```
Turning alternates which side of the fabric faces the viewer. Knotly tracks this change so that the right and wrong sides are represented correctly in the 3D preview.

> [!TIP]
> Use **Sketch mode** when reviewing rows. Its right- and wrong-side indicators and working-direction arrows make it easier to confirm that the work turns in the intended direction.

Another important use of the `turn` command is to create an oval as a foundation. First make a chain in `R0`, then crochet around it in a joined round:

```
R0: 9CH, turn  // Use 'turn' command to work next round back into the foundation chain
R1: 8X, W, 7X, V, $sl  // Crochet around the chain and close the round explicitly
```
The above example can be simplified to the following when round mode is set to **Joined rounds**:
```
R0: 9CH, turn  // Use 'turn' command to work next round back into the foundation chain
R1: 8X, W, 7X, V  // Drop '$sl' to keep it concise when on [Joined rounds] mode
```
