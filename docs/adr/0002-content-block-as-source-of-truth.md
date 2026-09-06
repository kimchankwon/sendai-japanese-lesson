# 0002. The lesson text lives in a plain-text block, not in the markup

## Context
Every phrase started life as hand-written HTML, so changing a word meant finding the right
`<div class="jp">` and getting `<ruby>` tags right. The teacher who owns this deck is not
the person who wrote it, and will be editing phrases up to and during the trip.

## Decision
All copy moves into a single plain-text Content Block inside `index.html`, in a line-based
format with no HTML, no quoting and no punctuation that breaks a file when omitted.
Furigana is authored as `漢字{かんじ}`. The Deck renders from that block at load. Edit Mode
edits the same model in place and Save File writes it back out.

## Reason
The alternative — a JSON or JS array — is denser to render from but fails destructively: a
missing comma yields a blank deck, with nothing on screen to explain why. This format
degrades to a per-line error message naming the line number, so a mistake made on a phone
at github.dev is visible and fixable. The cost is a hand-rolled parser and serialiser that
must round-trip exactly, since Save File depends on it.

Rejected: a separate `content.txt`. It reads cleaner, but browsers block `fetch` over
`file://`, which would break opening the deck straight from a USB stick — the one property
the deck was built to have.
