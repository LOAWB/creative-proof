# Liberty: one-line lockup (PEPTIDES dropped)

Jason, lane 2431 rowid 450848: "make a compliant version of this clients logo
remove peptides and just keep the word liberty". Source: libertypeptides.com.

## The brief's premise was wrong, and it made the job smaller

The routed task said *"PEPTIDES is WIDER than LIBERTY ... the whole thing needs
re-proportioning"*. Measured off the transparent source, that is not the case:

| element  | x range  | y range  | size    |
|----------|----------|----------|---------|
| mark     | 6..154   | 14..264  | 149x251 |
| LIBERTY  | 178..873 | 15..129  | 696x115 |
| PEPTIDES | 178..868 | 157..266 | 691x110 |

LIBERTY is **696** wide, PEPTIDES is **691**. LIBERTY is the wider of the two by
5px. The two lines are set to the same measure, so dropping PEPTIDES costs the
lockup no width and **the wordmark needed no re-proportioning at all**.

What was real: the mark is 251 tall against a 115-tall LIBERTY, so beside one
line it is 2.2x too tall and had to be rescaled and re-centred.

Also confirmed: the source is **886x281**, not the 2048x651 its filename claims.

## What was built

The type is never resampled. LIBERTY is placed at its native 696x115 crop, and
only the mark is scaled, always downward. The gap is held at the original 23px
because the gap belongs to the type, and the type has not changed size. (Scaling
the gap with the mark closed it to 11px and the word crowded the helix; that
was rendered, looked at, and rejected.)

| file | what it is |
|---|---|
| `liberty-lockup-primary.png` | 804x144. Mark at 1.25x the cap height. **The recommended one.** |
| `liberty-lockup-primary-reverse.png` | Same, mark's navy remapped to white, for dark backgrounds. |
| `liberty-lockup-alt-small-mark.png` | 787x115. Mark at 1.0x, the arithmetically faithful ratio. |
| `liberty-lockup-alt-large-mark.png` | 821x172. Mark at 1.5x, closest to the original's tall-anchor feel. |
| `liberty-wordmark-only.png` | 696x115. The wordmark alone, no mark. |

The mark is a tall narrow helix (w/h 0.59). Scaled to exactly the cap height it
collapses to 68px wide and reads as a sliver, which is why the faithful 1.0x is
the alternate and 1.25x is the recommendation. All five were rendered and
compared on white and on navy before choosing.

## Two things Jason should decide

1. **"Compliant" may need more than the word.** If the goal is ad-platform drug
   rejections, the DNA/helix mark still reads as pharma to a classifier. A
   neutralised mark is available but was deliberately **not** designed here,
   because nobody asked for a redesign. `liberty-wordmark-only.png` is the
   no-mark option if he wants to test without it.
2. **The original logo has no dark-background version.** On navy, the mark's
   navy dots and bars vanish and the ring centres are transparent holes, not
   white fill, so they fill with the background too. This is true of the
   client's existing artwork, not something introduced here.
   `liberty-lockup-primary-reverse.png` fixes it for the new lockup.

## Limits

Native-resolution raster. Print or large format needs the type rebuilt as
vector; this file must not be upscaled.

## Verify

`./check.sh` reads every deliverable with Vision at native size and at 2x and
asserts LIBERTY present, PEPTIDES absent, real alpha. The untouched source is
run as a control and must still read PEPTIDES, otherwise the absence checks
would be blind. Last run: **16 passed, 0 failed**.
