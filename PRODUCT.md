# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

One person: the author, who is also the only intended viewer. The page is opened in short glances through the day, on phone and on desktop, usually alongside other work. It has no second audience — no onboarding, no sharing flow, no explanation written for a stranger. The URL is public only because GitHub Pages is the cheapest way to keep a page online.

## Product Purpose

A time-measurement instrument. It states how far a fixed calendar interval has run, as a percentage carried to absurd precision and redrawn every animation frame. Success is being readable in one second and precise enough to be worth staring at while the last digits move. The dates carry no stated meaning on the page, and the page adds no encouragement, celebration, or urgency around them.

## Positioning

Ordinary countdowns round to days or seconds and stop there. This one treats the interval itself as the unit. The headline number is the share of the interval — four declared decimal places plus three fainter trailing digits that move faster than the eye resolves — while days, hours, minutes and seconds are demoted to secondary tiles, and a week/month axis shows where "now" sits between the start point and the target. The instrument framing is the part a generic countdown could not truthfully copy: declared precision versus shadow precision, a needle on a scale, and a footer that states the interval length and the size of one step.

## Operating Context

- One static `index.html` with inline `<style>` and `<script>`, deployed to GitHub Pages at https://ewtizz.github.io/tracker/ from the repository `Ewtizz/tracker`.
- Targets live as constants in the file (`START` and the `TRACKERS` array). Changing a date means editing those constants by hand and running `push.bat`, which stages everything, commits as `Update tracker page (<timestamp>)`, and pushes. **This stays the update workflow** — the page will not grow a UI for editing targets. `push.bat` is gitignored and exists only on the author's machine.
- Targets do change. History shows the target moved from 27 to 22 August, and a second tracker was added later. The dates in the file are working values, not fixtures.
- All times are the viewer's local time. There is no timezone handling and none is wanted.

## Capabilities and Constraints

Binding constraints, confirmed by the author:

- **Single file, no build.** Everything ships in one `index.html`: no bundler, no dependencies, no external requests, nothing that needs a step between editing and pushing.
- **Russian-only interface.** No localization, no language switch.
- **The seven-digit live percentage stays.** Four declared digits plus three faint trailing ones, redrawn on `requestAnimationFrame`. This is the signature of the page.

Shipped behavior to preserve unless a change is deliberate:

- Per-tracker `осталось / прошло` toggle, which reframes the readout, the lit portion of the scale, and the unit tiles together.
- A single shared start point (`START`) against which every tracker measures, so their percentages are comparable.
- The interval scale: weekly minor ticks, monthly major ticks with month labels, and a `сейчас` needle at the present moment.
- Four unit tiles (days / hours / minutes / seconds, seconds to hundredths).
- The footer stating start point, interval length in days and seconds, the step size of 1/10000 %, and what the faint digits resolve to.
- The "time to the next whole percent" caption, and the `is-over` state once a target has passed.

Open, deliberately undecided:

- **The number of trackers is not fixed.** Two exist today; one, or several, is a legitimate future state, and the layout should absorb that.
- **Theme control.** Dark is the default, a light palette exists under `prefers-color-scheme: light`, and a `data-theme` attribute on `:root` overrides both — but nothing in the interface sets it. The hook exists, the control does not.

## Brand Commitments

No name beyond the page title, no logo, no brand assets, no accounts. The voice is Russian, lowercase, terse and instrumental: `осталось`, `прошло`, `точка отсчёта`, `интервал`, `шаг 1/10000 %`, `бледные знаки`. It is never celebratory and never motivational. Typography relies on faces already present on the machine — Bahnschrift for display, Cascadia Mono for figures, Segoe UI Variable for text — with no webfont downloads, which follows from the no-external-requests constraint rather than from taste.

## Evidence on Hand

The running page and its git history are the only assets. There are no other users, no testimonials, no analytics, no metrics, no logo files, no photography, no copy deck. Future work must not invent any of these. It must also not name what the two dates commemorate: the author has not said, and the page deliberately does not say.

## Product Principles

1. **Precision is the product.** Anything that makes the number less exact, or less alive, is a regression.
2. **Instrument, not cheerleader.** No motivational copy, no celebration, no emotional framing of the dates.
3. **One file, no network.** Every addition has to survive being pasted into a single static document.
4. **Legible at a glance, rewarding on a stare.** The headline reads in a second; the faint digits pay off a longer look.
5. **Dates are data, not structure.** Which targets exist, and how many, will keep changing. The layout absorbs that without a rewrite.

## Accessibility & Inclusion

No formal standard was established, and there is no second user to establish one for. The product-specific facts that do hold: the page is used on both phone and desktop, so both stay in scope; `prefers-reduced-motion` already suppresses the pulsing dot and transitions while the per-frame digits keep running, because they are the content rather than decoration; the mode toggle uses real buttons with `aria-pressed`; the readout is `role="timer"` with `aria-live="off"` so a screen reader is not flooded by frame-rate updates; the scale is `aria-hidden`. Treat these as incumbent decisions to preserve, not as leftovers to clean up.
