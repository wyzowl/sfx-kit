# Using SFX Kit

How to find a sound, place it in time and fit it to a moment, and what the data says about each one. Written for AI
agents and tools as much as for people: everything here is also in the data, so a program can follow it too. How you
use the sounds, how many and how loud, is up to you.

## What you have

- `sounds/<category>/<id>.wav`: 320 sounds in 28 categories. WAV, 48 kHz, 24-bit; mono, or stereo
  that's centred (never panned).
- [`sounds.json`](sounds.json): every sound's data (described at the end). Load it to search and place sounds in code.
- [`catalogue.md`](catalogue.md): one line per sound, by category. Short enough to read whole.
- [`analysis.json`](analysis.json): detailed measurements (loudness, spectrum, stereo) if you want them.

## 1. Find

Start from what happens on screen: the table lists common moments with sounds made for them. Every row's sounds have
siblings in the catalogue (other intensities, lengths and variants), and each sound's `use_for`, `avoid_for` and
`tags` say what it suits.

| On screen | Sounds | Also |
| --- | --- | --- |
| Text, an icon or a card appears | `pop-small-in`, `pop-medium-in` | `appear-materialise` for a soft, magical entrance |
| Something disappears | `pop-small-out`, `appear-poof` | `appear-dissolve` for a soft exit |
| Items appear one by one (a list, bullet points) | `tone-step-1` to `tone-step-5`, rising in order | a soft pop for each |
| Something slides or moves across | `whoosh-fast-soft` (a move of 0.12 to 0.44 s), `whoosh-medium-soft` (0.28 to 0.81 s), `whoosh-slow-soft` (0.52 to 1.5 s) | medium and hard intensities for bigger, bolder moves |
| A quick flick, or a line or arrow drawing in | `swish-medium`, `zip-in-medium` | `zip-out-medium` for something leaving |
| A finger swiping in an app demo | `swipe-fast-soft`, `swipe-medium-firm` | |
| Something lands or settles | `impact-light-firm`, `impact-medium-soft` | heavier weights for bigger things |
| A big title or logo slams in | `cinematic-drum-big`, `impact-deep-hard` | `boom-hit-medium` and the other booms |
| A reveal after a build | `riser-2s-soft`, ending on `shimmer-medium-bright` or `boom-hit-medium` | the riser's sync point is its end |
| Something collapses or is pulled away | `reverse-whoosh-short-soft` | |
| A scene change | `whoosh-slow-medium`, or `reverse-whoosh-medium-soft` into the cut | |
| Zooming in or out | `move-zoom-in` (a zoom of 0.38 to 0.54 s), `move-zoom-out` | |
| A slow zoom or a camera push (a second or more) | `whoosh-slow-soft` for a push of up to 1.5 s | `riser-1s-soft` or `riser-2s-soft` when it builds to a reveal |
| Bouncing, springing or spinning | `move-bounce`, `move-spring`, `move-spin` | |
| A shape grows, shrinks or changes | `transform-grow`, `transform-shrink`, `transform-morph` | `transform-fill` for filling up |
| A card flips over to reveal | `appear-flip-quick`, `appear-flip-slow` | |
| A button pressed or a screen tapped | `click-button-medium`, `click-tap-medium` | `click-mouse-medium` for a cursor |
| A cursor hovering, a highlight moving | `click-hover-soft` | |
| A setting switching on or off | `click-toggle-on-medium`, `click-toggle-off-medium` | |
| Typing on a keyboard | `keyboard-typing-steady-medium` | `keyboard-letter-medium` per key, `keyboard-return-firm` for Enter |
| Typing on a phone | `click-tap-soft` on each character | `phone-keypad` for dialling a number |
| Handwriting, drawing, a tick | `writing-pen-write`, `writing-marker-draw`, `writing-pen-tick` | `writing-highlighter` to highlight |
| Done, correct, success | `notification-success-soft`, `notification-success-chime` | eight more successes |
| Wrong, an error | `notification-error-soft`, `notification-failure-knock` | eight more failures |
| A message arrives or is sent | `notification-message-in-soft`, `notification-message-out-soft` | |
| A phone buzzes or rings | `phone-vibrate-table`, `phone-ring-modern` | |
| A number counts up or down | `data-countup-medium`, `data-decrease-medium`, then `data-number-land` | three lengths of each |
| A chart or a bar appears | `data-chart-reveal`, `data-bar-grow` | `transform-grow` for a bar that grows for longer |
| Progress or loading | `data-progress-short`, `digital-process-subtle` | |
| Money, prices, payments | `money-register`, `money-coin-drop`, `money-card-tap` | |
| Time, deadlines | `time-clock`, `time-clock-fast`, `time-countdown` | |
| A highlight, something special | `shimmer-short-soft`, `tone-ding-mid` | |
| Celebrating a win | `celebration-popper`, `celebration-applause-small` | `celebration-fireworks` for the biggest |
| Technology at work: data, AI | `digital-scan-clear`, `digital-process-clear`, `digital-hacker` | |
| Errors, hacks, security | `digital-glitch-clear`, `digital-static`, `digital-denied`, `digital-breach` | `digital-decrypt` for access granted |
| A device switching on or off | `digital-power-up`, `digital-power-down` | |
| Paper, books, boxes, tools | `props-page-turn`, `props-box-open`, `props-scissors` | `foley-paper-touch` and the other materials |
| Locks, latches and machines | `mechanical-lock-light`, `mechanical-switch-heavy` | |
| An opening: the logo or title at the start | a long sting, such as `sting-bright-long` or `sting-airy-long`: its lead-in builds to the logo | `riser-1s-soft` into `shimmer-medium-bright` for a title |
| The logo at the end | `sting-warm-short` | seven characters (warm, bright, bold, minimal, playful, tech, airy) in two lengths; `shimmer-short-bright` for a logo less than a second before the end |

Within a category, the variants differ in the same ways:

- **Intensity:** soft and subtle variants are quieter and gentler, suited to calm, corporate or voiceover-led videos;
  harder ones are louder and sharper, suited to energetic edits.
- **Weight:** light, short sounds suit small elements; heavier, longer ones suit big things.
- **Length:** a sound that runs with an action, builds up to an arrival, follows a release or rides a move has
  `fits_seconds`: the length of moment it fits, within its rate range (section 4 says how to fit it exactly). Hits,
  pops and clicks don't have one: their length is only their ring.

## 2. Place

Every sound has a sync point, `sync.at`: the seconds from the start of its file to the part of it that should meet the
moment. Start every sound at

    start = (the moment it should meet) − sync.at

That's the only rule, and it works for every sound, because `sync.at` already points at the right part of each one:

- most sounds (hits, pops, clicks, whooshes, risers): their loudest moment;
- gestures with a length (typing, writing, swipes, counts, fills, applause): their very start, so they start with the
  action;
- sequences (a notification's notes, a phone's buzzes, the countdown's beeps): their first event, even when a later
  one is louder;
- sounds in parts: the part that matters (the till's bell, the card reader's beep, the flipped card's tap). `parts`
  lists the time of each.

`sync.meets` says what kind of moment the sync point meets, and `sync.how` says it for the sound. Where `sync.how`
says to start a sound with an action, it means the same thing: its sync point (where it becomes audible) meets the
action's first frame.

| `sync.meets` | The moment | For example |
| --- | --- | --- |
| `instant` | The frame something happens: a hit, a press, something appearing, landing or popping | impacts, pops, clicks, notifications |
| `action-start` | The frame an action begins; the sound runs with it | typing, writing, swipes, count-ups, shape changes |
| `move-peak` | A move's fastest point: the middle of an ease-in-out move, about a quarter of the way into an ease-out one (fast start), about three quarters into an ease-in one (fast exit) | whooshes, swishes |
| `arrival` | What a build leads to: the reveal, the cut, the landing | risers, reverse whooshes, zip ins, the zoom in, flips |
| `release` | The frame something is let go, dropped or sent off; the sound follows it | fallers, zip outs |

`timing` gives the rest of each sound's shape, in seconds from its start: `audible_start` (where it first comes within
40 dB of its peak), `onset` (within 20 dB), `peak` (its loudest moment), `body_end` (where it last falls 20 dB under)
and `audible_end` (40 dB under). Place by `sync.at`, not `timing.peak`: they differ for every sound that doesn't
anchor on its loudest moment.

- **Changing the rate** moves the times with it: divide `sync.at`, and every other time, by the rate. At rate 1.1, a
  sync point at 0.440 s comes at 0.400 s.
- **A start before 0** (a riser for a reveal in the first second): start the sound at 0 and trim that much off its
  beginning.
- **A whoosh and a landing:** a whoosh on a move it suits dies away just before the move ends, which leaves the
  landing clear for an impact.

## 3. Levels

Gains here are relative to each file as it is (0 dB).

- **Matched levels.** Every file sits on one loudness scale (`level.lufs`, its loudest 150 ms), so the sounds are
  level with each other as they are, and a category's intensities differ in level on purpose: soft is quieter than
  hard. `loudness` in `sounds.json` says how they're measured.
- **A reference.** At 0 dB, a medium effect's loudest moment is about −20.5 LUFS: a few dB under a voiceover mixed to
  about −16 LUFS integrated, a common level for online video.
- **Under speech.** `under_voiceover_db` (−1 to −8 dB) is how far a sound comes down, wherever its body
  (`timing.onset` to `timing.body_end`) overlaps speech, for the voice to stay clear over it. It's larger for sounds
  that compete more with a voice.
- **Sounds that cover a voice.** A sound whose `avoid_for` starts "On top of speech" masks or competes with a voice
  even when it's lowered: the bass-heavy sounds, stings, rings, the alarm, busy celebrations and noisy glitches.

## 4. Adapt

- **Rate:** `adapt.rate` is how far a sound can be slowed or sped up; its pitch moves with it, and so do its times
  (divide them by the rate). Sounds with `[1, 1]` keep their rate: the tuned ones, and a few whose pitch must stay
  true.
- **Fitting a length:** a sound that runs with an action, builds up to an arrival or follows a release has a
  `span_seconds`: the length of moment it fits at rate 1. The rate that fits a moment exactly is `span_seconds` ÷ the
  moment's length, within `adapt.rate` (`fits_seconds` is that range). A whoosh has no span: its `fits_seconds` are
  the lengths of move it suits.
- **Shortening:** a sound that runs with an action (`action-start`) can lose its end, where the action ends; a build
  that ends on its sync point (`arrival`) can lose its start instead. To drop a later part of a sound, cut just before
  that part's time in `parts`.
- **Trims and fades:** trims are in the file's own seconds (after a rate change, trimming t seconds takes t ÷ rate off
  the timeline). The files start and end on silence, so a cut part-way through a sound needs a short fade to avoid a
  click: 10 to 30 ms on a trimmed start, 20 to 50 ms on a cut end (300 ms or more for a long tail). `adapt.notes` says
  more for each sound.
- **Loops:** clocks, typing, applause, static and chatter loop well from their middle, with a short crossfade.
- **Tuning:** the tuned sounds are in C major, so they agree with each other, and each has a `tuning`. Most use only
  its pentatonic notes (C, D, E, G and A: `C major pentatonic`), which also sit with music in G or F major, or in A, E
  or D minor; three use a B or an F as well (`C major`), and the 808-style basses sit on C.

## An example

An app demo, six seconds, with a voiceover from 0.5 to 5.0 s:

- 0.8 to 1.3 s: a phone slides in from the right (ease-in-out) and lands.
- 2.3 s: a message badge pops onto it.
- 3.3 to 4.5 s: a number counts up from 0 to 1,200, landing at 4.5 s.
- 5.5 s: a tick appears beside it.

Each sound starts at its moment minus its sync point, and comes down by its `under_voiceover_db` where its body
overlaps the voiceover:

| Moment | Sound | Start | Under the voiceover |
| --- | --- | --- | --- |
| The slide, fastest at 1.05 s | `whoosh-medium-soft` (for moves of 0.28 to 0.81 s) | 1.05 − 0.229 = 0.821 s | −2 dB |
| The landing at 1.3 s | `impact-light-firm` | 1.3 − 0.011 = 1.289 s | −2 dB |
| The badge at 2.3 s | `notification-message-in-soft` | 2.3 − 0.046 = 2.254 s | −3 dB |
| The count, 3.3 to 4.5 s | `data-countup-medium` (it fits 1.01 to 1.43 s; at rate 1.214 ÷ 1.2 = 1.01, exactly 1.2 s) | 3.3 − 0.000 = 3.300 s | −2 dB |
| The number lands at 4.5 s | `data-number-land` | 4.5 − 0.011 = 4.489 s | −2 dB |
| The tick at 5.5 s | `notification-success-soft` | 5.5 − 0.000 = 5.500 s | none: the voiceover has ended |

## The data

[`sounds.json`](sounds.json) holds a summary of how to read and use the data (`how_to_use`), how its levels work
(`loudness`), its `categories` and a record for every sound. [`sounds.schema.json`](sounds.schema.json) describes it.

| Field | What it is |
| --- | --- |
| `id` | A stable identifier, which is also the file's name |
| `name` | A short name |
| `category` | Its category's id |
| `file` | The path to its WAV |
| `variant` | Its place in its category: speed, intensity, kind and so on |
| `description` | What it sounds like |
| `use_for`, `avoid_for` | The moments it suits, and the ones it doesn't |
| `tags` | Words to search by |
| `duration` | Its length in seconds |
| `channels` | 1 for mono, 2 for stereo |
| `sync` | `at` (its sync point, in seconds), `meets` (the kind of moment it meets) and `how` (that moment, for this sound) |
| `parts` | For a sound in parts: each part (`what`) and when it comes (`at`, in seconds) |
| `timing` | `audible_start`, `onset`, `peak`, `body_end` and `audible_end`, in seconds |
| `span_seconds` | For a sound that runs with an action, builds up to an arrival or follows a release: the length of moment it fits at rate 1 |
| `fits_seconds` | The length of moment it fits, within its rate range (not for hits, pops and clicks) |
| `level` | `lufs` (its loudest 150 ms), `true_peak_dbtp` and its `tier` |
| `under_voiceover_db` | How far it comes down where it overlaps speech |
| `adapt` | `rate` (how far its rate can change) and `notes` on fitting other lengths |
| `tuning` | For a tuned sound: `C major pentatonic`, `C major` or, for the 808-style basses, `C` |
| `pairs_with` | Categories it layers well with, and how |
| `character` | A word or two on its tone |
| `sha256` | The file's checksum |
