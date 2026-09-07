# 0003. Slides shrink their own type rather than sharing one safe size

## Context
Type had to get bigger, but the Deck's slides are not equally dense: a Phrase Slide holds
three lines while the Sendai facts slide holds six entries with descriptions. One global
size big enough for the phrase slides overflows the dense ones; one small enough for the
dense ones wastes the phrase slides, which are 19 of the 40.

## Decision
Set `--u0` generously (1.78vmin, up from 1.35vmin) and give each Slide an Auto-fit pass on
display that scales its own `--u` down until its content fits. Measured across all 40 slides
at 1920x1080 and 1440x900: 36 render at full size, 4 scale to 0.79-0.93, none overflow.

## Reason
The alternative is picking one number and hand-checking every slide after every copy edit —
and the deck is explicitly built to be edited by someone who will not re-check all 40. Auto-fit
makes overflow structurally impossible instead of a thing to remember, which matters more
here than every slide sharing an identical type size.

The cost is honest: type size now varies between slides, so two slides seen back to back can
differ by up to a fifth. The fit only ever shrinks, never grows, so a sparse slide can never
balloon past the intended scale.

Note for future edits: this was worth doing only after fixing the real cause of the overflow.
`.bullets`, `.toc`, `.vocab` and `.facts` capped their width in `ch`, which resolves against
the container's own inherited 16px rather than the ~55px type inside them — so those columns
were rendering about 356px wide, roughly twelve characters per line. Those max-widths are now
expressed in `--u`. Auto-fit should stay a safety net, not a substitute for that kind of bug.
