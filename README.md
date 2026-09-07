# 仙台 · Sendai Missions Japanese Lesson

A 60-minute beginner Japanese deck for a short-term missions team going to Sendai.

**Live:** https://kimchankwon.github.io/sendai-japanese-lesson/

## Presenting

Open `index.html`. No build step, no network, no dependencies — it works off a USB stick
in a classroom with no wifi.

| Key | Does |
| --- | --- |
| `→` `←` / space | Next / previous slide |
| `F` | Fullscreen |
| `C` | Cheat sheet |
| `E` | Edit mode |
| `S` | Download an updated `index.html` with your edits |
| `R` | Discard local edits |
| `Home` / `End` | First / last slide |

Swipe works on touch. The URL hash tracks the slide, so `#12` deep-links.

## The cheat sheet

A second view of the same deck at `#sheet` — every phrase in one scrolling, printable
page, grouped by section. It is linked from the title slide and from the closing
reminders slide, reachable with `C` from anywhere, and has a Print button that switches
to black-on-white in two columns.

On a phone it drops to one column with a compact sticky header, so the phrases stay
thumb-scrollable in the street. It is **generated from the same content block as the slides**, so it cannot fall out of
step with them. Add a phrase to the deck and it appears on the sheet; there is no second
copy to maintain. Any slide can link to it by adding `link: <button label>`.

## Editing the lesson

All the words live in one plain-text block near the top of `index.html`, marked
`<script id="content">`. There is no HTML in it. Two ways to change it:

**On GitHub — nothing to install.** Open the repo, press `.`, and a full editor opens in
your browser. Edit the block, commit, and the live site redeploys in about a minute.

**In the deck itself.** Press `E`, click any line, type. Edits save to your browser as you
go. Press `S` to download an `index.html` containing them, then replace the file in the
repo. Press `R` to throw the edits away.

### The format

```
=== phrase | aoba
sec: あいさつ
romaji: Arigatou gozaimasu
jp: ありがとうございます
en: Thank you
note: Say the long **o**: a-ri-ga-**too**.
```

- `=== <type> | <colour>` starts a slide
- `key: value` sets a field
- `key:` on its own (no value) opens a named list
- `- a | b | c` is a list row, split on `|`
- `#` starts a comment

Furigana is `漢字{かんじ}`, which renders as ruby text above the kanji. `**bold**`,
`*highlight*` and `___` (a styled blank) also work.

Types: `title` `toc` `bullets` `facts` `divider` `phrase` `practice` `vocab`.
`link: <label>` on any slide adds a button through to the cheat sheet.
Colours: `aoba` `sakura` `sora` `murasaki` `hi` `kin`.
Add `opt: yes` to mark a slide optional.

If the block has a typo, the deck shows the line number and what it expected instead of
failing silently.

## What's in it

40 slides across nine sections: Expectations, About Sendai, Greetings, Your name, What you
study or do, Your hobby, When you're stuck, Church words, Put it together — then a reminders
slide, and three optional "If time" slides at the end.

Twenty phrases are drilled inside the hour (the **Core Twenty**). Six prompt-only
**Practice Slides** are spaced through the deck; the teacher runs the timing.

Every phrase shows romaji first and largest, then Japanese with furigana, then English —
the students cannot read kana and have one hour.

## Design decisions

`CONTEXT.md` holds the vocabulary this deck is built on. `docs/adr/` holds decisions that
were deliberate rather than obvious.
