# tangentscraps/cardinalrule

> "A little game about a bird" — a Ludum Dare-era NES-style game written in
> **Flash Pascal** (Pascal that compiles to Flash SWF): a Joust × Defender
> hybrid where you're a cardinal fending off vampire bats. The Flixel side is
> a stub; the playable sprite test survives.
> Repo: https://github.com/tangentscraps/cardinalrule — commits Nov 2012,
> by Michal Wallace. Play the Godot port:
> https://tangentstorm.github.io/arcade/cardinalrule/#play/cardinalrule/direct
> **Keep, document.**

## What it is

The README describes the design clearly: an NES-style game combining two
Williams Electronics classics — [Joust](http://en.wikipedia.org/wiki/Joust_%28video_game%29)
and [Defender](http://en.wikipedia.org/wiki/Defender_%28video_game%29). The
environment and objective follow Defender (a wide, wrap-around scrolling
landscape; protect things on the ground from enemies trying to snatch them),
while combat follows Joust (press to flap; when you collide with a bat,
whoever is higher wins). The twist: instead of a spaceship, you're a
**cardinal**, and instead of aliens, **vampire bats**.

The distinctive technical choice is the language: **Flash Pascal**
([flashpascal.sourceforge.net](http://flashpascal.sourceforge.net/)), a
Pascal compiler targeting the Flash VM — hence the unusual mix of `.pas`
and `.as` files. `src/Flx.pas` and `src/crule.pas` wrap Flixel (the AS3
game framework, included as a submodule) in Pascal `external class`
declarations; `spritetest.pas` is a working sprite demo. The pure-AS3 side
never got past scaffolding — `src/PlayState.as` literally adds the text
`"INSERT GAME HERE"`.

The playable artifact is `spritetest.pas`: it loads `img/cardinal-r.png`
(the cardinal sprite) through a `MovieClipLoader`, scales it 2×, and gives
it velocity + gravity (0.2/frame) controlled by the arrow keys, at 512×448
and 32 fps. `game.html` embeds the resulting `spritetest.swf`. So the repo
contains the bird, the physics feel, and the design doc — but not the bats,
the scrolling landscape, or the Joust-style collision.

The commits run Nov 24–25, 2012 ("resized swf to NES size per the ludum dare
rules" — the 256×224 internal resolution, doubled to 512×448). The game has
since been ported to Godot and is playable in the browser:
https://tangentstorm.github.io/arcade/cardinalrule/#play/cardinalrule/direct

(Flagged as unverified: the commit message says "per the ludum dare rules"
but no Ludum Dare event number is recorded in the repo; the late-November
2012 dates fall just before that December's event, but which event (if any)
this was entered in is not documented.)

## Tech stack

Flash Pascal → SWF; Flixel (AS3, git submodule); FlashDevelop project
(`Cardinalrule.as3proj`); MIT/x11 license per the README. The Godot port
lives separately under the arcade site.

## Inventory

| Path | Contents |
|------|----------|
| `README.md` | Game design: Joust × Defender, cardinal vs vampire bats, Flash Pascal credit |
| `src/spritetest.pas` | Working sprite test: loads cardinal PNG, arrow-key velocity, gravity |
| `src/crule.pas`, `src/Flx.pas` | Pascal wrappers around Flixel classes (`external class`) |
| `src/CardinalRule.as`, `src/PlayState.as`, `src/MenuState.as`, `src/Preloader.as` | AS3/Flixel side — PlayState is an "INSERT GAME HERE" stub |
| `img/cardinal-r.png` | The cardinal sprite |
| `game.html` | Embeds `spritetest.swf` at 512×448 |
| `Cardinalrule.as3proj` | FlashDevelop project (SWF 512×448) |
| `.gitmodules` | Flixel submodule |

## Surprising / notable

- **Flash Pascal is the real story.** Writing a Ludum Dare game in Pascal-
  to-Flash in 2012 — while everyone else used raw AS3 — is exactly his kind
  of contrarian tooling choice, and the `external class` wrappers are a neat
  FFI pattern.
- **Design doc survived, game didn't:** the README's Joust-meets-Defender
  pitch is vivid and complete; the code has the bird but no bats. The Godot
  port is where the design finally became playable.
- **The sprite test is the game feel prototype:** gravity, velocity,
  arrow-key flight — the Joust half of the design was being prototyped
  before the Defender half existed.
- No linked streams or videos found in the repo. Verdict at triage: **keep +
  document** (done — this file).

## Verdict

Keep, document. The repo is a design document plus a tech demo for an
unusual toolchain; the playable realization is the Godot port linked above.
If the Flash Pascal angle ever becomes a story (a "weird tools I have
shipped games in" post), this is exhibit A.
