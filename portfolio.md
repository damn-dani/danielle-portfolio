# Portfolio — Progress Log

> **How to resume:** Say "pickup portfolio.md". Claude should: (1) read this whole file, (2) `Read` the current `index.html` to confirm it matches what's described here, (3) open it with `open index.html`, (4) give Danielle a plain-language summary of what was last done and where things stand, and (5) end with a **TO DO** section listing anything left incomplete — even if that list is empty, say so explicitly.

## Git status (check before assuming anything is live)
Last known state: pushed to `origin/main` via `git push --force-with-lease` on 2026-09-24 (commit `1f0f8fa`), after reconciling a diverged remote commit (see below). Always run `git status`/`git log` to confirm this is still accurate — don't trust this line blindly if time has passed.

**Repo:** `/Users/daniellenaidu/Documents/danielle-portfolio` (git remote: `damn-dani/danielle-portfolio` on GitHub)
**Live site:** https://damn-dani.github.io/danielle-portfolio/ — **NOT yet updated**, all work below is local only, not committed/pushed.
**Single file:** `index.html` (no build step, no framework, plain HTML/CSS/JS).
**Note:** There is a second, unrelated local copy at `~/Copywriting Portfolio/danielle-portfolio` — that is NOT the one we're editing. Always use the Documents path above.

## Why this redesign happened
Danielle got a new job — **Editorial & Marketing Coordinator, 1105 Media** (covers *Security Today*, *Campus Security Today*, *EP Online*, *OH&S*). The site's purpose changed from a freelance-client pitch to a **professional portfolio/CV** (confirmed decision — do not reintroduce "hire me" freelance-sales language like the old "Process" methodology section or the "Built with Claude — I can build one for you too" pitch).

## Content decisions (facts, not to re-derive)
- Work email: `dnaidu@1105media.com` — labeled "Work"
- Personal/networking email: `daniellenaidu.co@gmail.com` — labeled "Personal & Networking"
- Both are separate `mailto:` links in the Contact section; the copy-to-clipboard JS fallback handles both (loops `a[href^="mailto:"]`, copies whichever address was clicked).
- **Published Work** section: 12 real bylined articles (3 per outlet), all verified genuinely written by Danielle via direct article fetch (title/byline/date confirmed) — do NOT trust web-search summaries for this kind of claim again, they hallucinated specific fabricated article titles earlier in this project; only trust a direct per-article fetch.
- Background timeline now leads with "2026 – Present · Editorial & Marketing Coordinator — 1105 Media"; the 4-item logo strip is 1105 Media, Odisee, WPP, EssenceMediacom (in that order).
- Contact sub-line (current wording, replacing the old generic "Open to freelance projects..." line):
  > "Always up for a good story, a sharp campaign, or a conversation about either. Based in Sandton, South Africa — remote-ready, and happy to pack a bag if the opportunity's right."

## Sections removed (deliberately — don't re-add without asking)
- "Process" / 4-phase methodology section (agency-pitch fluff)
- "Built with Claude" freelance web-design pitch strip
- "Graphics & Content" / Gallery section (Beauty Brand, Skincare, Reading Princess carousel images) — removed per Danielle's explicit request

## Current design system ("Warm & Bold" — chosen after comparing 4 palette options in a published artifact)
- **Colors:** paper `#FBF6EE`, paper2 `#F5EDDD`, ink `#1A1A1A`, accent `#E8590C` (burnt orange), accent2 `#1C6E5E` (teal). Dark sections use `#1A1A1A`.
- **Fonts:** Fraunces (serif/display — has the editorial, slightly playful italic used for emphasis words), DM Sans (body), IBM Plex Mono (small caps labels, eyebrows, dates — gives editorial/punchy texture).
- **Hero:** solid dark CTA button (not just underline), photo tilted 2° with a hard offset orange drop-shadow (`box-shadow: 10px 12px 0 var(--accent)`), role label has a teal underline.
- **Eyebrows:** pill-shaped mono badges (bullet + text in a bordered pill), not plain text labels.
- **Four publications:** shown as colorful stamp-style badges (`.badge.badge-1/2/3/4`, orange/teal/gold/brick-red) — used both in the strip under the hero AND as the outlet headers inside Published Work, for visual consistency.
  - **Note:** could not find downloadable/reusable logo image files on the actual publication sites (they use styled text mastheads, not logo images) — used the colored text badges instead of real logos to avoid any trademark-reuse ambiguity. Danielle was told this; she may still want real logos revisited later if she can source the actual files herself.

## History note — a real conflict happened here, resolved 2026-09-24
Before the 2026-09-24 push, `origin/main` had a July 21, 2026 commit (`7c81180`) that was never merged into this session's working copy — it added a **"Five Brands" spec-copywriting section** and a **GoVocal/CitizenLab internship + testimonial** in the Background timeline, plus a nav-overflow fix. Danielle decided: **restore the GoVocal internship** (done — it's now in the timeline with its testimonial) and **drop the spec-copywriting section** (real bylines now do that job instead). Local history was then force-pushed over the remote's diverged commit. If anything else from that old commit turns out to be missing and wanted, it's recoverable via `git show 7c81180:index.html` even after the force-push (it's still in GitHub's reflog/network for a while).

## TO DO
1. Real publication logos — still using colored text badges as a stand-in, not actual logo image files (see note above). Revisit if Danielle sources the real logo files herself.
2. There are several untracked files sitting in the repo (extra PDFs/PNGs, `.DS_Store`, `.scratch/`) unrelated to this task — left alone, not part of git. Ask before touching them.
3. One earlier oddity: `git status`/`git fetch` hung for 1-2 minutes a couple of times mid-session, then worked fine on retry. Not investigated further — if it recurs, just retry rather than assuming something is broken.

## How to verify changes visually (headless screenshot gotchas)
The site uses scroll-triggered reveal animations (`.r` class, IntersectionObserver) that a plain headless screenshot won't trigger. To preview:
```bash
cp index.html /tmp/preview.html
python3 -c "
with open('/tmp/preview.html') as f: c = f.read()
c = c.replace('</style>', '.r{opacity:1!important;transform:none!important}</style>')
with open('/tmp/preview.html','w') as f: f.write(c)
"
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless --disable-gpu \
  --run-all-compositor-stages-before-draw --virtual-time-budget=5000 \
  --screenshot=/tmp/final.png --window-size=1440,7200 "file:///tmp/preview.html"
```
(Without the longer virtual-time-budget, images can appear broken in the screenshot — that's a timing artifact, not a real bug; assets load fine in an actual browser.)

## Section map (nav anchors)
`#hero` → `#published` (Published Work) → `#skills` (Core Skills) → `#work` (Fanta + Reading Princess case studies) → `#background` (education/timeline/certs) → `#contact`
