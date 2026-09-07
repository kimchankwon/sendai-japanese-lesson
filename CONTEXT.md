# CONTEXT

Glossary for the Sendai short-term missions Japanese lesson (60 minutes, absolute beginners).

## Deck
The single self-contained HTML file that is the entire deliverable. Runs offline, arrow-key navigation, no build step and no network. _Avoid_: "slides" (ambiguous between the file and its pages), "presentation".

## Slide
One page of the Deck. Every Slide is exactly one of: Phrase Slide, Practice Slide, or Concept Slide.

## Phrase Slide
Teaches one Japanese phrase. Carries a Phrase Card and nothing else of substance.

## Phrase Card
The three-line unit every phrase is rendered as, in fixed order:
1. **Romaji** — largest, the line students read aloud
2. **Japanese** — kanji with furigana where kanji appears, otherwise plain kana
3. **English** — smallest

_Avoid_: "translation block", "phrase box".

## Practice Slide
A prompt-only exercise Slide: it states the task the pairs perform and shows no scripted A/B lines and no timer. The teacher runs the timing. _Avoid_: "activity slide", "exercise card".

## Concept Slide
A Slide carrying an idea rather than language — the Expectations slides, the TOC, the conclusion.

## Fill Frame
A sentence pattern with a blank where the vocabulary goes, taught before the vocabulary that
fills it. `Shumi wa __ desu` is a Fill Frame. The blank is written `__` in both the romaji and
the Japanese line and renders as a styled gap. _Avoid_: "template sentence", "pattern drill".
The Deck used to speak the blank aloud as まるまる (maru maru); that was dropped, so don't
reintroduce it in one slide without doing all of them.

## Romaji-Primary
The rule that Romaji is the visually dominant line on every Phrase Card, because this cohort cannot read kana and has 60 minutes. Kana and furigana are present for exposure and for the trip, not for in-lesson decoding.

## Breakdown Set
The four Phrase Slides for a conversation that has already failed: toilet, "I don't understand
Japanese", "once more please", "do you speak English". Chosen over transactional or social
phrases because a student who is stuck needs an exit, not a shop. _Avoid_: "survival phrases"
(too broad — implies the transactional set too).

## If-Time Slide
A Slide after the conclusion that is not part of the 60 minutes and is skipped by default.
Currently only the Christian invitation and gospel-vocabulary phrases live here. Visually
marked so the teacher can see at a glance that it is optional. _Avoid_: "appendix", "bonus".

## Core Twenty
The 20 phrases drilled inside the hour: 4 greetings, 2 name, 2 study, 2 work, 2 hobby,
4 breakdown, 3 church words, 1 self-identification. Was the Core Eighteen until work got its
own two Phrase Slides. The count is meant to be argued over before it grows again — every
addition spends repetition time, which is the scarce thing in a 60-minute lesson, not slides.

## Content Block
The plain-text `<script id="content">` region of `index.html` holding every word in the
Deck. It is the source of truth: the Deck is rendered from it at load, and Save File
writes the edited model back into it. No HTML lives here. _Avoid_: "the data", "config".

## Furigana Braces
The authoring syntax `漢字{かんじ}` in the Content Block, rendered to `<ruby>` at load.
Chosen so a non-technical editor can add readings without touching markup.

## Edit Mode
The state entered with `E`, in which every Phrase Card line and list cell becomes directly
typeable on the slide. Editable elements show their **raw** Content Block text — braces and
asterisks visible — never the rendered form, so what is typed is what is stored.

## Save File
The export from Edit Mode: serialises the in-memory model back into Content Block syntax,
splices it into a clone of the page, and downloads a complete replacement `index.html`.
_Avoid_: "publish", "deploy" — it downloads a file; committing it is a separate act.

## Slide Unit
`--u`, the single length every type size, gap and padding in the Deck is a multiple of.
`--u0` is the root value; a Slide may override `--u` below it to fit. Nothing in the
stylesheet sets a px font-size, so one number changes the whole Deck's scale.

## Auto-fit
The measure-and-shrink pass run on a Slide when it becomes visible: if its content is taller
than the Slide, `--u` is scaled down until it fits, then left alone. Sparse Slides therefore
render at full size and dense ones only give up what they must. It never scales *up*.

## Cheat Sheet
The second view of the Deck, routed at `#sheet`: every Phrase Card in one scrolling,
printable page grouped by section. It is *derived* from the same Content Block the slides
render from and holds no copy of its own, so it cannot drift. Reached by `C`, or from any
Slide carrying a `link:` field. _Avoid_: "handout", "reference page" — and never let it
become a second place phrases are written down.

## Route
The part of the URL hash that selects a view: a slide number, or `sheet`. It must be read
once before the first render, because `show()` rewrites the hash as soon as a slide is
displayed. Two separate bugs have come from reading it later.
