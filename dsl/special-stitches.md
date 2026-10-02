# Special Stitches

Special stitches add texture, raised details, and decorative edges to a pattern. Knotly has dedicated commands for puffs, bobbles, and popcorns. Picots and shells are built by combining ordinary stitch and position commands. Pay attention to stitch counts: a puff, bobble, or popcorn has several components but counts as one finished stitch, while a shell produces several finished stitches.

## Puffs and bobbles

Puffs and bobbles are textured, 3D crochet stitches created by grouping multiple unfinished stitches into a single space and closing them together so they pop out from the fabric.

Use `puff` for a puff made from half double crochet components or `bobble` for a taller bobble made from double crochet components. In XVA notation, `Q` is the shorthand for the default puff; changing the parameter can also make it a taller bobble.

By default, a puff in Knotly consists of four half-double crochet stitches, whereas a bobble consists of four double crochet stitches when no size is specified.

| Command | Default components | Finished stitch count |
|---|---|---:|
| `puff` or `Q` | Four half double crochets (`4hdc`) | 1 |
| `bobble` | Four double crochets (`4dc`) | 1 |

Place the command where the textured stitch should appear in the sequence. For example, `R3` alternates an ordinary single crochet with a puff six times:

```
R0: mr
R1: 6sc
R2: 6sc2inc
R3: 6(sc, puff)
```

`R2` produces 12 stitches. `R3` consumes all 12 root stitches and produces 12 final stitches: six single crochets and six puffs. To make the raised stitches taller, replace `puff` with `bobble`.

To control the number and type of components, add a parameter in square brackets immediately following the command. Write the number before the component stitch, as in `puff[5hdc]`, `bobble[5dc]`, or `Q[5T]`. This tells Knotly to override the command’s default components with those specified in the parameter. Mixed stitch types are not supported within a parameter for a puff or bobble.

| XVA notation | U.S. terminology | What is constructs |
|---|---|---:|
| `Q` | `puff` | A puff stitch of four half-double crochet stitches |
| `Q[4F]` | `bobble` | A bobble stitch of four double crochet stitches |
| `Q[5T]` | `puff[5hdc]` | A puff stitch of five half-double crochet stitches |
| `Q[5F]` | `bobble[5dc]` | A bobble stitch of five double crochet stitches |

Knotly allows up to eight components in one puff or bobble. The component count only affects its appearance, not the number of final stitches it contributes to the round or row.

## Popcorns

Like a puff or bobble, a popcorn is a raised, 3D stitch, but it is constructed differently. Work several complete stitches into the same space, remove the hook from the last stitch, then draw its live loop through the first stitch to join them. Puffs and bobbles, by contrast, bring unfinished stitch components together before closing them.

Use `popcorn` in U.S. terminology or `G` in XVA notation for popcorn stitch. By default, each popcorn has five double crochet components (`5dc`):

```
R3: 6(sc, popcorn)
```

As in the puff example above, this line works across 12 root stitches and produces 12 final stitches. Each `popcorn` uses one root stitch and counts as one final stitch, even though its bump contains five components.

| XVA notation | U.S. terminology | What is constructs |
|---|---|---:|
| `G` | `popcorn` | A popcorn stitch of five double crochet stitches |
| `G[4F]` | `popcorn[4dc]` | A popcorn stitch of four double crochet stitches |
| `G[6E]` | `popcorn[6tr]` | A popcorn stitch of six treble crochet stitches |

Like a `puff` or `bobble` command, you can specify another size or stitch type with a bracketed parameter, such as `popcorn[4dc]` or `G[4F]`. The same eight-component limit and non-mixed-type rule apply. Choose a popcorn when you want a more prominent bump, or use a puff or bobble for a softer, more clustered texture.

## Picots

A picot is a small pointed loop, usually made from a short chain anchored near its starting point. Knotly has no separate picot command because a picot is essetially made from several basic stitches. Anchor the chain at one root stitch, make three to five chains, then attach it to the next root stitch with a slip stitch or, in some designs, a single crochet:

```
R1: 6sc
R2: 6sc2inc
R3: 6(sl, 3ch, sl)
```

In `R3`, each group of `(sl, 3ch, sl)` produces a complete picot: the first slip stitch attaches to one root stitch, the three chains extend outward without consuming any, and the second slip stitch anchors the chain back to `R2` at the next root stitch. They form six evenly spaced picot loops around the edge. Change the number of chains to adjust their size.

## Shells

A shell is a fan of several stitches worked into one root stitch. It is a decorative increase, not a separate Knotly command. Use a [compound increase](/docs/dsl/shaping#compound-increases-and-decreases) to make a shell of mixed stitch types.

This example arranges five graduated shells around a foundation chain ring:

```
# Assuming the current round mode is set to [Joined rounds]
R0: 10ch
R1: 5(sk, [hdc, dc, tr, dc, hdc]+)  // Work five shells into the chain loop
```

In **Joined rounds** mode, `R0` forms a loop of ten chains. `R1` repeats two steps five times: `sk` or `K` passes over one root chain position, then `[hdc, dc, tr, dc, hdc]+` — or `[T, F, E, F, T]+` in XVA — works all five stitches into the next position. The stitches rise from half double crochet to treble crochet and then descend again, giving each shell its characteristic fan shape.

Each repetition uses two chain positions and produces five stitches. The five repetitions use all ten positions in `R0`, producing the 25 stitches shown in the counter gutter. The skipped positions separate the shells, while the chain loop leaves an opening at the center. Together, these elements create a star-shaped motif.

The brackets are essential to make a shell: `[hdc, dc, tr, dc, hdc]+` works all five component stitches into one root stitch. If written as an ordinary comma-separated sequence, they would be worked into successive positions instead. Change the component stitches or add chain spaces between shells to vary the fan shape and openness of the fabric, and [check the stitch counts](/docs/quick-start#know-your-stitch-counts) before adding another round.
