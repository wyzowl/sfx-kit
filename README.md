# SFX Kit

Also on Hugging Face: [huggingface.co/datasets/wyzowl/sfx-kit](https://huggingface.co/datasets/wyzowl/sfx-kit).

320 original sound effects for videos, animations and interfaces, made to be as easy for AI tools to use as for
people. Every sound comes with the data needed to choose it, place it in time and mix it: what it is, when to use it
and when not to, its length, its sync point and its level.

Free for any use, commercial or not: [CC0](LICENSE), no credit required.

## What's inside

| Category | Sounds | What it's for |
| --- | --: | --- |
| [Whooshes](catalogue.md#whooshes) | 9 | Movement, sliding, flying and transitions |
| [Swishes and zips](catalogue.md#swishes-and-zips) | 9 | Quick, sharp movement: flicks, cuts, and things zipping in or out |
| [Swipes](catalogue.md#swipes) | 6 | Fingers swiping across screens: app demos, cards and carousels |
| [Reverse whooshes](catalogue.md#reverse-whooshes) | 6 | Air drawn in to a sudden stop: things collapsing into a point, and the build into a cut |
| [Risers and fallers](catalogue.md#risers-and-fallers) | 12 | Building anticipation before a reveal, and things descending or leaving |
| [Bounce, spin and zoom](catalogue.md#bounce-spin-zoom) | 5 | Bouncing, springing, spinning and zooming |
| [Impacts](catalogue.md#impacts) | 12 | Objects landing, colliding and hitting |
| [Cinematic hits](catalogue.md#cinematic-hits) | 8 | Big, bass-heavy hits for title slams, trailer beats and dramatic moments |
| [Booms and bass](catalogue.md#booms-and-bass) | 15 | Deep booms and drops, sub drops, 808s and rumbles, for big reveals, title cards and scene changes |
| [Pops](catalogue.md#pops) | 9 | Elements appearing, scaling and popping into view |
| [Appear and vanish](catalogue.md#appear-and-vanish) | 6 | Things vanishing in a puff, dissolving, materialising, flipping over and bursting |
| [Shape changes](catalogue.md#shape-changes) | 8 | Shapes and icons growing, shrinking, morphing, stretching, inflating and filling |
| [Interface](catalogue.md#interface) | 36 | Clicks, taps, toggles and switches, snaps, clips, claps and hovers |
| [Keyboard](catalogue.md#keyboard) | 15 | Typing, keypresses and text entry |
| [Writing and drawing](catalogue.md#writing-and-drawing) | 16 | Pens, pencils, markers and chalk: writing, drawing and ticking, erasing and highlighting |
| [Phone](catalogue.md#phone) | 5 | Phones vibrating, ringing and dialling |
| [Mechanical](catalogue.md#mechanical) | 12 | Locks, latches, switches, shutters and other mechanisms |
| [Foley](catalogue.md#foley) | 12 | Paper, card, fabric, plastic, glass and wood being handled |
| [Everyday props](catalogue.md#everyday-props) | 10 | Pages, books, scissors, tape, boxes, zips, bells and water |
| [Notifications](catalogue.md#notifications) | 28 | Success and failure, errors, alerts, messages and attention |
| [Tones](catalogue.md#tones) | 8 | Single notes: a ding for highlights, and steps that rise as text or list items appear |
| [Shimmers](catalogue.md#shimmers) | 9 | Highlights, sparkles and positive reveals |
| [Logo stings](catalogue.md#logo-stings) | 14 | Short signatures for logo reveals, end cards and title moments |
| [Celebration](catalogue.md#celebration) | 5 | Applause, party poppers, confetti and fireworks |
| [Time](catalogue.md#time) | 6 | Clocks ticking, alarms, timers, stopwatches and countdowns |
| [Money](catalogue.md#money) | 7 | Coins, a till, paying by card and counting notes |
| [Digital](catalogue.md#digital) | 20 | Scanning, processing, glitches, static and data security |
| [Data](catalogue.md#data) | 12 | Count-ups, progress, bars, charts and numbers landing |

Every sound is a WAV file (48 kHz, 24-bit), 67 MB in all.

## Quick start

**For AI tools and agents.** Read [GUIDE.md](GUIDE.md), which maps on-screen moments to sounds and explains placing
and fitting them, and [catalogue.md](catalogue.md), with one line per sound. For code, load
[sounds.json](sounds.json). Then:

1. **Find** a sound by what happens on screen: its `use_for`, `avoid_for` and `tags` say where it fits, and its
   `fits_seconds` what length of moment.
2. **Place** it so its sync point meets the moment: start it at that moment minus its `sync.at`. That one rule works
   for every sound.
3. **Levels:** the sounds are matched in loudness as they are, and each says how far it comes down under speech
   (`under_voiceover_db`).

**For people.** Browse `sounds/` by category, or search [catalogue.md](catalogue.md) for a word.

## The data

- [sounds.json](sounds.json): how to read and use the data, in brief, its categories, and a record for every sound: name,
  description, uses and things to avoid, tags, length, sync point and the moment it meets, timing, the length of
  moment it fits, level, how far it can be adapted, tuning, and what it layers well with.
  [sounds.schema.json](sounds.schema.json) describes it.
- [catalogue.md](catalogue.md): every sound in one line each, to read when choosing.
- [analysis.json](analysis.json): each sound's detailed measurements (loudness, spectrum, stereo image).

## The standard

| | |
| --- | --- |
| Format | WAV, 24-bit, 48 kHz; mono, or stereo that's centred and never panned |
| Loudness | Matched across the kit on one scale (the loudest 150 ms, K-weighted, in LUFS), with each category's intensities apart from each other |
| Peaks | True peak at or under −3 dBTP, no clipping |
| Ends | Trimmed close, starting and ending on silence, without clicks |
| Low end | Cut to what each sound needs, so nothing rumbles under a voice except the bass sounds, which are meant to |

## How they're made

Every sound is synthesised by code: struck materials, air, friction, bubbles and tuned instruments, modelled on how
real things make sound, and clean electronic tones for the sounds that are digital by nature. No recordings, samples
or other sound libraries went into any of them. The sounds, and the code that makes them, were created with Claude,
Anthropic's AI model, directed by Wyzowl, and every one was listened to and approved before release.

## Licence

[CC0 1.0 Universal](LICENSE): no rights reserved. Use the sounds and the data for anything, commercial or not, change
them, and share them, with no need to ask or credit. If you'd like to give credit, though, it's welcome: "SFX Kit by
Wyzowl".

Version 1.0.0.
