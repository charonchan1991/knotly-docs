# Quick Start

This guide walks you through the basic workflow for turning written crochet instructions into a 3D preview. If you are new to Knotly, try beginning with a small project and run the simulation after every few rounds or rows. Short feedback loops make syntax and shaping problems much easier to find.

## Select your terminology

Knotly’s instruction language supports both **XVA notation** and **U.S. crochet terminology**.
XVA is a letter-based shorthand notation system widely used in East Asia. Its characters visually represent the structure of stitches. For example, `X`, the symbol for a single crochet, resembles the crossed strands of the stitch, while `V`, the symbol for an increase, represents two stitches branching from one.

U.S. terminology, by contrast, uses abbreviations derived from English stitch names. It is generally easier for English speakers to read and understand, although it can be more verbose.

The following table lists the equivalent stitches and operations in XVA notation and U.S. terminology:

| Stitch or command | XVA notation | U.S. terminology |
|---|---:|---:|
| Magic ring | `MR` | `mr` |
| Chain stitch | `CH` | `ch` |
| Slip stitch | `SL` | `sl` / `ss` |
| Single crochet | `X` | `sc` |
| Half double crochet | `T` | `hdc` |
| Double crochet | `F` | `dc` |
| Treble crochet | `E` | `tr` |
| Two-stitch single crochet increase | `V` / `XV` | `sc2inc` |
| Two-stitch half double crochet increase | `TV` | `hdc2inc` |
| Two-stitch double crochet increase | `FV` | `dc2inc` |
| Two-stitch treble crochet increase | `EV` | `tr2inc` |
| Three-stitch single crochet increase | `W` / `XW` | `sc3inc` |
| Three-stitch half double crochet increase | `TW` | `hdc3inc` |
| Three-stitch double crochet increase | `FW` | `dc3inc` |
| Three-stitch treble crochet increase | `EW` | `tr3inc` |
| Single crochet two together | `A` / `XA`| `sc2tog` / `sc2dec` |
| Half double crochet two together | `TA` | `hdc2tog` / `hdc2dec` |
| Double crochet two together | `FA` | `dc2tog` / `dc2dec` |
| Treble crochet two together | `EA` | `tr2tog` / `tr2dec` |
| Single crochet three together | `M` / `XM` | `sc3tog` / `sc3dec` |
| Half double crochet three together | `TM` | `hdc3tog` / `hdc3dec` |
| Double crochet three together | `FM` | `dc3tog` / `dc3dec` |
| Treble crochet three together | `EM` | `tr3tog` / `tr3dec` |
| Puff / Bobble stitch | `Q` | `puff` / `bobble` |
| Popcorn stitch | `G` | `popcorn` |
| Skip | `K` | `sk` |

> [!TIP]
> While Knotly’s instruction language is case-insensitive, we recommend following its case conventions: *UPPERCASE* letters for **XVA notation** and *lowercase* letters for **U.S. terms** and other commands.

You can mix the two systems within the same project, but using only one is recommended to avoid ambiguity and improve readability. Choose the system you are most familiar and comfortable with, and use it consistently throughout your project.

> [!TIP]
> Knotly includes a built-in notation control that lets you convert between the two systems. Set your **preferred terminology** to either system above. When Knotly detects that your pattern text uses a different notation system, you will be able to convert it to your preferred one in the editor panel.

## Know your pattern editor

The pattern editor is a collapsible panel on the left side of the main canvas. It is where you’ll do most of your work. Use the **Edit project** button in the panel’s title bar to update your project details. This option is not available when you’re viewing someone else’s project. The button at the upper right of the title bar collapses the panel to give you more room to interact with the 3D models. On smaller screens, the panel collapses automatically when you run a pattern.

You can switch between parts using the dropdown in the pattern editor. A badge next to the dropdown shows the project’s status: <span class="sync-status"><span class="badge pending"><span class="dot"></span>Pending</span></span> / <span class="sync-status"><span class="badge synced"><span class="dot"></span>Synced</span></span> / <span class="sync-status"><span class="badge unsynced"><span class="dot"></span>Unsynced</span></span>.

<span class="sync-status"><span class="badge synced"><span class="dot"></span>Synced</span></span> suggests all models in the scene are up to date, whereas <span class="sync-status"><span class="badge unsynced"><span class="dot"></span>Unsynced</span></span> indicates at least one part has changed and the preview needs a re-run. Look for a green or orange dot at the end of each part’s title line if you need to know the sync status of that part.

The counter gutter to the right of the main editing area shows the stitch total for each instruction line. If a line has a warning or error, expand its counter to see the details. For more information on the counter gutter, see [Know your stitch counts](#know-your-stitch-counts) below.

At the bottom of the editor, use the **Default round mode** button to set the project’s [end-of-round behavior](./dsl/fundamentals.md#round-modes-and-end-of-round-controls). The **Format pattern text** button beside it opens the formatter popup that helps you [clean up your pattern text](#clean-up-with-formatter).

After making changes, click **Run** to rerun the simulation and update the 3D preview.

> [!TIP]
> The editor also supports a few useful shortcuts: use <kbd><kbd>Ctrl</kbd> + <kbd>Enter</kbd></kbd> — or <kbd><kbd>Command</kbd> + <kbd>Enter</kbd></kbd> on macOS — to run the pattern, and <kbd><kbd>Ctrl</kbd> + <kbd>S</kbd></kbd> or <kbd><kbd>Command</kbd> + <kbd>S</kbd></kbd> to save a project.

## Know your stitch counts

Understanding stitch counts is essential before you begin. The phrase “number of stitches in a round or row” can be ambiguous because an instruction line generally has two different stitch counts — although in most cases, it refers to the total number of stitches a line produces.

When reviewing a stitch command, distinguish between the number of stitches it **consumes** and the number it **produces**:
- **Stitches consumed** are the stitches used from the preceding round or row. They are sometimes referred to as the **root stitches** of an instruction line by Knotly.
- **Stitches produced** are the new stitches created to form the foundation of the next round or row. They are sometimes referred to as the **final stitches** of an instruction line by Knotly.

The following table shows the numbers of stitches consumed and produced by several common stitches and commands:

| Stitch or command | Notation (XVA / U.S.) | # stitches consumed | # stitches produced |
| --- | ---: | ---: | ---: |
| Single crochet | `X` / `sc` | 1 | 1 |
| Two-stitch single crochet increase | `V` / `sc2inc` | 1 | 2 |
| Three-stitch single crochet increase | `W` / `sc3inc` | 1 | 3 |
| Single crochet two together | `A` / `sc2tog` | 2 | 1 |
| Single crochet three together | `M` / `sc3tog` | 3 | 1 |
| Chain stitch | `CH` / `ch` | 0 | 1 |
| Skip | `K` / `sk` | 1 | 0 |

The total number of stitches produced by each instruction line is displayed in the counter gutter on the right side of the editor. You do not need to track this manually — Knotly recalculates the count for each round or row as you type.

```
# Check counter gutter on the right for the number of stitches each line produces 
R1:	6sc  // (6)
R2:	6sc2inc  // (12)
```

In most cases, the total number of stitches consumed by an instruction line should match the number produced by the preceding line.

When these numbers differ, Knotly alerts you with either an error or a warning. If an instruction line requires more stitches than are available in the preceding round or row, Knotly reports an error indicating how many stitches exceed the available count (the number of root stitches). If stitches remain unused, it displays a warning indicating how many root stitches remain available.

When an alert appears, expand the counter to compare the number of stitches consumed with the number available and identify potential problems.

```
P1: Example for round overflowing
R1:	6 sc
R2:	8 sc2inc  // Check counter gutter for an error

P2: Example for round finishing early
R1:	6 sc
R2:	4 sc2inc  // Check counter gutter for a warning
```
A warning does not always indicate a mistake. Some constructions intentionally leave stitches unused, particularly when creating openings, branches, or partial rows.

## Start writing

A Knotly pattern is organized into parts, rounds or rows, and comma-separated instructions. Each loose part becomes an object in the scene.

The following single-part pattern is enough to try the complete edit-and-preview workflow. With **Joined rounds** selected, paste it into the editor and click **Run**:

```
R1: 6X
R2: 6V
R3: 6(X, V)
R4-R6: 18X
R7: 6(X, A)
R8: 6A
```
This pattern text will generate a very basic but interactive ball in the main canvas. To learn more about how to write instructions in Knotly, see [Instruction Language: Fundamentals](./dsl/fundamentals.md).

### Break down your project to parts

Treat each separately constructed piece as a part. In a no-sew design, features worked continuously can remain within the same part. For example, the body, head, ears, and tail of an amigurumi figure would usually be separate parts. Give each part a unique `P` code and, optionally, a descriptive name:

```
P1: Body
R1: 6X
R2: 6V
R3: 6(X, V)
// ...

P2: Head
R1: 6X
R2: 6V
// ...
```

Keep the instructions for a part immediately below its heading. Part numbers do not have to be consecutive, but numbering parts in the order in which they are made keeps references easy to follow. Use clear titles as well; both codes and titles appear in the editor's selection dropdown and beside selected objects in the scene.

For a single-piece project, you can omit the part heading and let Knotly use the default part code `P0`. Add explicit part heading lines as soon as the project has multiple pieces or when another instruction needs to refer to a particular part.

### Determine foundation & round mode

Before writing the first regular line, decide how the part begins and how each line ends. The project’s default **round mode** supplies the end-of-round behavior whenever an instruction line does not specify one explicitly:

| Construction | Round mode | Default foundation | End-of-round command |
| --- | --- | --- | --- |
| Closed circular rounds | **Joined rounds** | Magic ring | `$sl` / `$ss` |
| Uninterrupted spiral | **Continuous rounds** | Magic ring | `-$sl` / `-$ss` |
| Back and forth | **Rows** | Foundation chain | `turn` |

**Joined rounds** is the default and closes each round automatically. **Continuous rounds** carries the work directly into the next line without a closing join. **Rows** turns the work after each line so the next row proceeds in the opposite direction.

`R0` defines the foundation and `R1` begins the regular stitching. Knotly can infer a magic ring in **Joined rounds** mode and a matching foundation chain in **Rows** mode, but writing `R0` explicitly makes the construction easier to understand. It is required whenever the foundation differs from the mode’s default, such as a fixed chain ring:

```
# Assuming the current round mode is set to [Joined rounds]
R0: 12CH  // This creates a chain ring, overriding the default
R1: 6(X, V)
```

You can override the default mode for a line with an [end-of-round command](./dsl/fundamentals.md#round-modes-and-end-of-round-controls). Use `$sl` / `$ss` to close a round, `-$sl` / `-$ss` to leave it open, or `turn` to reverse the working direction for the next round or row.

For a complete guidance, see [Starting a part](./dsl/writing-instructions.md#starting-a-part).

### Preview as you edit

Work in small sections and click **Run**  to update the 3D preview whenever you make changes. The editor’s status badge shows whether the preview is in sync with your instructions and when you need to run the pattern again. If Knotly encounters a parsing error, it displays a message below the editor and highlights the error’s location in the instructions.

Switch between the render modes to evaluate your design:

- **Sketch** exposes the underlying construction, working direction, and front or back side of the fabric
- **Chart** shows standard crochet symbols and is useful for checking stitch types and placement
- **Realistic** gives the clearest impression of the final material, color, and overall silhouette

See [Working with render modes](./essentials.md#working-with-render-modes) for a detailed introduction. 

When the shape does not look right, return to the last round or row that previewed correctly. Compare its produced count with the number consumed by the next line, then inspect the placement of increases, decreases, skips, and turns. Add one or two lines at a time; move on when you are happy with the preview. This is usually faster than debugging a completed pattern all at once.



### Assemble

There are generally two ways to assemble multiple parts into a complete project. One obvious way is to move and rotate each part manually until the parts are properly aligned. This approach gives you precise control over their relative positions and rotations, as well as greater flexibility to experiment with different arrangements.

This method is generally faster to simulate because the interactions between parts remain simple. However, because each part is simulated independently, the parts do not influence one another’s shape. This may not matter when the parts are simply attached or glued together, but some construction methods can cause connected parts to affect one another’s shaping.

In these cases, you may want to simulate all the parts together as a single object. Sewing or joining them is a good approach because these commands automatically group the connected parts into one object, allowing the physics engine to simulate their interactions instead of treating them as separate, loose parts. Because this increases the structural complexity, the simulation may take slightly longer to complete than the first approach. See [Multi-part Objects](./dsl/multi-part.md) for complete guidance.

Parts built from existing stitches from another part are also structurally connected, so this technique can be used to assemble multiple parts as well:

```
P1: Base
R1: 6X
R2: 6V
R3-R5: 12X

P2: Ruffle
R0: P1R5
R6: FLO, 12FW  // Continuing on the front loops of P1R5
```

Here, `P2` uses all stitches in `P1R5` as its foundation, so the base and ruffle are simulated as one whole. See [Begin with existing stitches](./dsl/writing-instructions.md#begin-with-existing-stitches) for details.


### Clean up with formatter

Open **Format pattern text** from the brush button at the bottom of the editor panel. The formatter can:

- Normalize round codes and update selectors that refer to them
- Merge adjacent rounds with identical instructions into a round range
- Combine consecutive identical stitches using coefficients
- Apply case conventions for XVA and U.S. terminology

Enable the actions you want the formatter to perform and click **Format now**. If you prefer the same cleanup every time you run a preview, enable **Auto-format on run**. Formatting changes how the pattern is written but should not affect the final 3D preview. However, it is generally a good practice to review the result before continuing, especially if your project uses selectors, joins, or sewing commands that reference specific rounds.

Formatting is most useful after the structure is working. During early experimentation, keeping similar rounds on separate lines can make changes easier; once the shape is stable, the formatter can condense them into a cleaner pattern without changing the intended construction.
